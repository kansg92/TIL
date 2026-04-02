# BFCache



뒤로가기후  api호출이 안되는 버그가 있었음.

알고 보니 브라우저가 BFCahce로 저장되어서 해당 페이지를 snapshot으로 가지고있어 vue `onMounted` 쪽 함수가 씹혔던것... 

```javascript
window.addEventListener('pageshow', function(event) {
  if (event.persisted) {
    // bfcache에서 페이지가 복원됨
  }
});
```

위 코드를 통해 BFCahce를 제어할 수 있었음.

문제가 하나 더 발생했는데 가상좀이 형성 되기전 `loadData`가 되었고.. 그걸 고치기 위해 vue `nextTick()` 함수 실행 후 `loadData()`가 작동 되도록 변경함.





## BFCache란 무엇인가요?

BFCache는 backwards/forwards 캐시의 약자로, 브라우저에서 렌더링된 페이지의 전체 스냅샷을 메모리에 보관하는 메커니즘입니다.

즉, 뒤로 또는 앞으로 이동할 때, 웹 페이지가 로딩 시간 없이 거의 즉시 렌더링됩니다.

BFCache가 없으면 브라우저는 전체 웹페이지를 처음부터 로드해야 하므로 서버에 다시 연결해 모든 정적 에셋을 다시 다운로드하고 모든 스크립트를 다시 실행해야합니다

하지만, BFCache를 사용한다면 빠르고 원활하게 전환 가능합니다.

## BFCache 동작 방식

BFCache는 전체 웹페이지의 스냅샷을 찍어 메모리에 저장합니다. 여기서 **실행되던 자바스크립트 코드는 어떻게 될지** 의문이 들 수 있습니다.

매우 좋은 질문입니다. 왜냐하면, BFCache 작동 방식은 전체 자바스크립트 힙이 메모리에 저장되고 진행 중인 코드의 실행이 일시 중지되기 때문입니다. 즉, setInterval 또는 setTimeout으로 실행이 예약된 코드는 아무 일도 없었던 것처럼 BFCache에서 페이지가 제공될 때 다시 시작됩니다. 이행되지 않은 프로미스도 마찬가지입니다.

indexedDB 트랜잭션을 다룰 때 동작은 조금 더 까다로워지는 경향이 있습니다.

트랜잭션이 진행 중일 때 사용자가 페이지에서 다른 곳으로 이동하면 사용자가 떠나기 전에 연결이 닫히지 않는 한 브라우저는 BFCache에 페이지를 캐시하지 않습니다.

일반적으로 브라우저는 사용자의 편에 서서 합리적이라고 판단되는 경우에만 웹페이지를 BFCache에 캐시 합니다.

대부분의 주요 브라우저는 모바일과 데스크톱 모두에서 어떤 형태로든 BFCache를 지원합니다.

크롬 사용 데이터에 따르면 데스크톱에서는 네비게이션 중 10건 중 1건, 모바일에서는 5건 중 1건이 뒤로 또는 앞으로 이동하는 것으로 나타났습니다. 이 수치는 매우 방대하므로 BFCache는 실제로 상당한 시간을 절약할 수 있는 잠재력을 가지고 있습니다.



## 웹페이지를 BFCache와 호환되도록 만들기

이제 BFCache가 사용자가 다시 웹사이트로 더 빠르고 원활하게 돌아올 수 있도록 한다는 점은 모두 이해하셨을겁니다.

하지만 개발자의 입장에서는 BFCache가 종종 좌절의 원인이 될 수 있으므로 몇 가지 고려 사항에 유의해야 합니다. BFCache에서 제공되는 페이지의 수명 주기 이벤트를 알아두는 것이 중요합니다.

페이지 **load** 이벤트는 BFCache에서 페이지가 로드될 때 발생하지 않습니다. 따라서 **pageshow** 이벤트를 수신해야 하며, `event.persisted` 속성을 확인하여 페이지가 BFCache에서 복원되었는지 확인할 수 있습니다. 이는 데이터가 오래되었는지 감지하는 데 유용할 수 있으며, 예를 들어 API 호출을 수행하여 업데이트할 수 있습니다.

```javascript
window.addEventListener('pageshow', function(event) {
  if (event.persisted) {
    // bfcache에서 페이지가 복원됨
  }
});
```

unload 이벤트 수신과 같은 일부 작업은 페이지가 BFCache에 들어가지 못하게 하므로 대신 pagehide 이벤트를 수신하고 unload 이벤트 리스너를 항상 추가하지 않도록 하세요. unload 이벤트는 이전부터 사용되어 왔으며 현재 레거시 API로 간주됩니다.

> 이 API는 레거시 API로 간주되므로 항상 **unload** 이벤트를 수신하지 마십시오.

예를 들어 레딧에서와 같이 웹서버가 **Cache-control: no-store** 헤더를 전송하면 브라우저는 BFCache를 건너뛰도록 지시받습니다. 기술적으로 이 헤더는 HTTP 캐시에만 사용되어야 하고 BFCache는 HTTP 캐시가 아니므로 이 동작은 변경될 것입니다.

> BFCache에 대해 더 자세히 알고 싶으시다면 다음 글을 읽어보세요!
> [Back and forward cache | Articles | web.dev](https://web.dev/articles/bfcache?ref=sabatino.dev)

## 테스트

우수한 사용자 경험을 보장하려면 BFCache를 자주 테스트하는 것이 중요합니다.

크롬 개발도구를 열고 애플리케이션 탭으로 이동한 다음 Back/forward cache를 클릭하면 BFCache를 쉽게 테스트할 수 있습니다. 이 페이지에서 커다란 'Test back/forward cache 버튼'을 누르면 크롬이 자동으로 웹페이지로 이동했다가 다시 돌아와 페이지가 캐시에 진입했는지 여부를 표시합니다.





### 참고 문서

https://kghworks.tistory.com/117

https://velog.io/@superlipbalm/bfcache

https://ko.vuejs.org/api/general