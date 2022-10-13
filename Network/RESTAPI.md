# 📢REST API



## REST 란??

### REST의 정의

- Representational State Transfer 의 약자로 대표적인 상태 전달을 뜻한다.
- 즉, 자원(resource)의 표현(representation) 에 의한 상태 전달
  1. 자원(resource)의 표현(representation)
     - 자원: 해당 소프트웨어가 관리하는 모든 것
     - -> Ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
     - 자원의 표현: 그 자원을 표현하기 위한 이름
     - -> Ex) DB의 학생 정보가 자원일 때, ‘students’를 자원의 표현으로 정한다.
  2. 상태(정보) 전달
     - 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.
     - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
- 월드 와이드 웹(www)과 같은 분산 파이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식이다.
  - REST는 기본적으로 웹의 기존 기술 HTTP 프로토콜을 그대로 활하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
  - REST는 네트워크 상에서 Client 와 Server 사이의 통신 방식 중 하나이다.



#### 구체적인 개념

- HTTP URL(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(Post,Get,Put,Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

- 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.

  - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
  - CRUD Operation
    - Create : 생성(POST)
    - Read : 조회(GET)
    - Update : 수정(PUT)
    - Delete : 삭제(DELETE)
    - HEAD: header 정보 조회(HEAD)

- 즉, REST는 자원 기반의 구조 (ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고, HTTP Method를 통해 REsource를 처리하도록 설계된 아키텍처를 의미한다.

- 웹 사이트의 이미지, 텍스트 DB 내용 등의 모든 자원에 고유한 ID인 HTTP URL를 부여한다.

  

#### REST 의 장단점.

##### 장점

- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화 해준다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- HTTP 프로토콜 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

##### 단점

- 표준이 존재하지 않는다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL 보다 Header 값이 어렵게 느껴질 수 있다.
- 사용할 수 있는 메소드가 4가지 밖에 없다.
  - HTTP Method 형태가 제한적이다.

- 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
  - PUT, DELETE 를 사용하지 못하는 점
  - pushState를 지원하지 않는 점(history_pushState - 뒤로가기)
    - URL를 통한 ServerSide Rendering 방식을 이용하게 된다면
      - 메인 페이지 -> 보드1페이지 -> 보드5페이지 클릭 -> 뒤로가기 -> 보드1페이지
    - REST 방식을 이용하게 된다면
      - 메인 페이지 -> 보드1 페이지 -> 보드5 페이지 클릭 -> 뒤로가기 -> 메인페이지

#### REST가 필요한 이유

1. ‘애플리케이션 분리 및 통합’
2. ‘다양한 클라이언트의 등장’
3. 최근의 서버 프로그램은 다양한 브라우저와 안드로이폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
4. 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.

#### REST 구성 요소

1. 자원(Resource): URI
   - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
   - 자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
   - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
2. 행위(Verb): HTTP Method
   - HTTP 프로토콜의 Method를 사용한다.
   - HTTP 프로토콜은 GET, POST, PUT, DELETE 와 같은 메서드를 제공한다.
3. 표현(Representation of Resource)
   - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
   - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
   - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

#### REST의 특징

1. Server-Client(서버 클라이언트 구조)

   - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.

     - Rest Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.

     - Client : 사용자 인증이나 context(세션, 로그인 정보) 등을 직적 관리하고 책임 진다.

   - 서로 간 의존성이 줄어든다.

2. Stateless(무상태성)
   - cookie를 이용해 session을 서버에 저장했다면, rest는 header에 token을 넣어 인증하고 세션을 저장하지 않는다.

3. Cacheable(캐시 처리 가능)
   - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
     - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
     - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
   - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
   - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
4. Layered System(계층화)
   - Client는 REST API Server만 호출한다.
   - REST Server는 다중 계층으로 구성될 수 있다.
     - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
     - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
   - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
5. Code-On-Demand(optional)
   - Server로부터 스크립트를 받아서 Client에서 실행한다.
   - 반드시 충족할 필요는 없다.
6. Uniform Interface(인터페이스 일관성)
   - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
   - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
     - 특정 언어나 기술에 종속되지 않는다.



## REST API란

- API(Application Programming Interface)란
  - 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능 하도록 하는것
- REST API의 정의
  - REST 기반으로 서비스 API를 구현하는 것
  - 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능 하다록 만든 아키텍쳐) 등을 제공하는 업체 대부분은 REST API를 제공한다.



#### REST API 특징

- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
- 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.



## RESTful이란

#### RESTful 개념

- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
- ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
  - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.



#### RESTful의 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

#### RESTful하지 못한 경우

- Ex1) CRUD 기능을 모두 POST로만 처리하는 API
- Ex2) route에 resource, id 외의 정보가 들어가는 경우(/students/updateName)



###### 참고자료

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

https://www.slipp.net/wiki/pages/viewpage.action?pageId=12878219
http://mygumi.tistory.com/55
https://brainbackdoor.tistory.com/53
http://tech.devgear.co.kr/delphi_news/433404
https://meetup.toast.com/posts/92
https://spoqa.github.io/2012/02/27/rest-introduction.html
https://hackernoon.com/build-restful-api-in-go-and-mongodb-5e7f2ec4be94
https://docs.oracle.com/cd/E76467_01/alloc/pdf/141/html/operations_guide/alloc-og_restful-impl.htm
https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html