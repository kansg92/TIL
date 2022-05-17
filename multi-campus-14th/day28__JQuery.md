# 📢day28__JQuery

## JQuery



### jQuery란?

- 2006년 1월 존 레식(John Resig)이 BarCamp NYC에서 발표
- jQuery는 자바스크립트 라이브러리 중 하나이다.
- JavaScript programming을 아주 쉽고 빠르게 작업이 가능하다.
- jQuery는 비교적 배우기 쉽다.
- jQuery는 오픈소스 라이브러리 이다.
  - [Jquery 공식 사이트](http://www.jquery.org)
- 다양한 함수와 플러그인을 제공한다
- JavaScirpt 와 jQuery를 함께 사용하여 프로그램을 진행.



### jQuery의 특징

- jQuery는 JavaScript 라이브러이의 일종으로 기존에 JavaScript를 보다 빠르고 안정적으로 개발이 가능하다.
  - 이벤트 처리가 쉽다.
  - HTML DOM 관련처리가 쉽다.
  - CSS 관련 처리가 쉽다.
  - AJAX 관련 처리가 쉽다.
  - 모든 브라우저에서 통일하게 동작 한다.
  - 다양한 플러그인을 제공 한다.

### jQuery 설치

- CDN(Content Delivery Network)방식 이용

  - 특정 서버에서 실시간으로 동작 시 다운받아 라이브러리를 웹페이지에 설치하여 사용

  - 단, 외부 인터넷 망이 막혀 있는 사이트에서는 사용불가.

  - jquery 버전에 유의해야함.

    ```html
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    ```

    

### jQuery syntax

- $ 사용을 통한 jQuery코딩
- $()을 통해서 HTML요소를 찾을 수 있다.
- `$(selector).action();`

```javascript
$(document).ready(function(){
	$('#hh1').css('color', 'red');
});
```

