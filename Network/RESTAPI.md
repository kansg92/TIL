# 📢REST API



## REST 란??

### REST의 정의

- Representational State Transfer 의 약자로 대표적인 상태 전달을 뜻한다.
- 월드 와이드 웹(www)과 같은 분산 파이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식이다.
  - REST는 기본적으로 웹의 기존 기술 HTTP 프로토콜을 그대로 활하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
  - REST는 네트워크 상에서 Client 와 Server 사이의 통신 방식 중 하나이다.



#### 구체적인 개념

- HTTP URL(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(Post,Get,Put,Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
- 즉, REST는 자원 기반의 구조 (ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고, HTTP Method를 통해 REsource를 처리하도록 설계된 아키텍처를 의미한다.
- 웹 사이트의 이미지, 텍스트 DB 내용 등의 모든 자원에 고유한 ID인 HTTP URL를 부여한다.



#### REST 의 장단점.

##### 장점

- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화 해준다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- HTTP 프로토콜 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.

##### 단점

- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL 보다 Header 값이 어렵게 느껴질 수 있다.
- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
  - PUT, DELETE 를 사용하지 못하는 점
  - pushState를 지원하지 않는 점(history_pushState - 뒤로가기)
    - URL를 통한 ServerSide Rendering 방식을 이용하게 된다면
      - 메인 페이지 -> 보드1페이지 -> 보드5페이지 클릭 -> 뒤로가기 -> 보드1페이지
    - REST 방식을 이용하게 된다면
      - 메인 페이지 -> 보드1 페이지 -> 보드5 페이지 클릭 -> 뒤로가기 -> 메인페이지



#### REST의 특징

- Server-Client(서버 클라이언트 구조)
- Stateless(무상태성)
  - cookie를 이용해 session을 서버에 저장했다면, rest는 header에 token을 넣어 인증하고 세션을 저장하지 않는다.
- Cacheable(캐시 처리 가능)