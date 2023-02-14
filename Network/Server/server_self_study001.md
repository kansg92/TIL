# 서버 공부01

## SSL(Secure Socket Layer)



### SSL Function in tel OSI Model

![ssl1](https://blog.lael.be/wp-content/uploads/2016/10/ssl1.png)

SSL을 세션계층(Layer 5), 표형계층(Layer 6), 응용계층(Layer 7)으로 보통 분류하기 때문에 SSL은 Layer4 ~ Layer7 사이에 있다.

[^OSI 모델]: Open Systems Interconnection 모델 ( OSI 모델 ) 은 &#39;시스템 상호 연결을 위한 [ISO\] 표준 개발 조정을 위한 공통 기반을 제공&#39;하는 개념적 모델 입니다. [2\] OSI 참조 모델에서 컴퓨팅 시스템 간의 통신은 물리적, 데이터 링크, 네트워크, 전송, 세션, 프레젠테이션 및 응용 프로그램의 7가지 추상화 계층으로 나뉩니다. 

| [계층](https://en.wikipedia.org/wiki/Abstraction_layer) 별 OSI 모델 |
| ------------------------------------------------------------ |
| 보여주다7. [애플리케이션 계층](https://en.wikipedia.org/wiki/Application_layer) |
| 보여주다6. [프레젠테이션 레이어](https://en.wikipedia.org/wiki/Presentation_layer) |
| 보여주다5. [세션 계층](https://en.wikipedia.org/wiki/Session_layer) |
| 보여주다4. [전송 계층](https://en.wikipedia.org/wiki/Transport_layer) |
| 보여주다3. [네트워크 계층](https://en.wikipedia.org/wiki/Network_layer) |
| 보여주다2. [데이터 링크 계층](https://en.wikipedia.org/wiki/Data_link_layer) |
| 보여주다1. [물리적 계층](https://en.wikipedia.org/wiki/Physical_layer) |

### 어떻게 SSL은 암호화 통신하는가?

- SSL은 보안인증서라고 말할 수 있다.
- 인터넷에서 보안인증서란 암호화코드가 내장된 주민등록증이라 볼 수 있다.

![ssl2](https://blog.lael.be/wp-content/uploads/2016/10/ssl2.png)

1. 클라이언트가 서버에 접속한다
2. 서버가 보안인증서를 제공한다
3. 클라이언트가 서버가 제출한 보안인증서의 유효성을 파악한다. 최상위 발급 기관과 통신하여 유효성을 확인한다.
4. 보안인증서가 유효하면 인증서에 쓰여져 있는 공개 암호화키 A를 사용하여 클라이언트가 자신의 공개 암호화키 C를 암호화 하여 전송한다.
5. 서버는 전송된 암호화 구문을 자신만 가지고 있는 해독키(개인 비밀키) B를 통해서 해독한다
6. 해독한 메세지가 유효한 요청이고 클라이언트의 공개 암호화키 C를 포함하고 있다면 암호화키 C를 사용하여 잘 받았다는 메세지를 암호화해서 응답한다.
7. 클이언트는 자신만 가지고 있는 해독키(개인 비밀키) D를 통해서 해독한다. 서버에서 받은 응답 메시지가 유효하다면 클라이언트는 A를 통해 암호화해서 메세지를 보내고, 서버는 C를 통해 암호화해서 메세지를 보낸다. A키로 암호화된 메세지는 B키로만 해독이 가능하고, C키로 암호화된 메세지는 D키로만 해독이 가능하므로 서로 종단간(End to End) 암호화 통신이 성립된다.

SSL이 적용된 사이트는 "종단감 암호화" 가 적용되기 때문에 중간 패킷 감청으로부터 안전하다.(해독키가 없으면 메시지 해석이 불가능.)
