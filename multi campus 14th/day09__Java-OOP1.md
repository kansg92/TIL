# 📢day09__Java class

### 객체 지향 프로그래밍(Object Oriented Programming) 

#### OOP개념

- 요구사항정의 -> OOAD -> OOP

- OOAD(Obecjt Oriented Analysis and Desigin) 개념에서 출발하였고, UML (Unified Modeling Language)에서 시발점이 되었다. 해당 개념을 JAVA에서 구현하면서 OOP(Object Oriented Programming)개념을 만들었다.

[OOAD 개념](https://soniacomp.medium.com/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%A0%81-%EB%B6%84%EC%84%9D%EA%B3%BC-%EB%94%94%EC%9E%90%EC%9D%B8-object-oriented-analysis-and-design-%EC%86%8C%EA%B0%9C-part-1-%EB%B2%88%EC%97%AD-67ff58fd26c9)

[UML 개념](https://www.microsoft.com/ko-kr/microsoft-365/business-insights-ideas/resources/guide-to-uml-diagramming-and-database-modeling)

- OOP란 부품에 해당하는 객체들을 먼저 만들고, 이것들을 하나씩 조립해서 완성된 프로그램을 만드는 기법을 말한다.

- 객체지향언어 도서 추천 : [헤드 퍼스트 디자인 패턴 - 한빛미디어](https://book.naver.com/bookdb/book_detail.naver?bid=22236366)

#### OOP 특징

- Encapsulcation
  - 객체의 필드, 메소드를 하나로 묶고, 실제 구현 내용을 감추는 것을 말한다.
  - 외부 객체는 객체 내부의 구조를 알지 못하며 객체가 노출해서 제공하는 필드와 메소드만 이용할 수 있다.
  - 필드와 메소드를 캡슐화 하여 보호하는 이유는 외부의 잘못된 사용으로 인해 객체가 손상되지 않도록 하는데 있다.
  - [캡슐화란 무엇인가?](https://javacpro.tistory.com/31)
- Inheritance
  - 상속
- Polymorpism
  - 다형성
- Abstraction
  - 추상화

#### 객체(Object)란?

- 물리적으로 존재하거나(자동차, 사람, 책 등) 추상적으로 생각할 수 있는 것(회사, 날짜, 계좌 등) 중 자신의 속성을 가지고 있고 다른 것과 식별 가능한 것을 말한다.
- 자바의 객체는 필드(속성)과 메소드(동작)로 구성되어 있다.
- 현실세계의 객체를 소프트웨어 객체로 설계하는 것을 객체 모델링(Object Modeling)이라고 한다.
-  Object Modeling은 현실 세계 객체의 속성과 동작을 추러내어 소프트웨어 객체의 필드와 메소드로 정희하는 과정이라 볼 수 있다.

##### 자동차의 Object Modling

```java
// 자동차 객체
public class Car { 
	// Attribute (속성, 필드)
	String name;
	String color;
	int size;
	int fsize;
	int cfsize;

	//Constructor(생성자): 생성자의 이름은 Class이름과 같아야한다.
	public Car() {
		this.name = "k3";
		this.color = "white";
		this.size = 1000;
		this.fsize = 50;
		this.cfsize = 0;
	}        

	// Operation (동작, 매소드)
	public void go() {
		System.out.println("Go !");
	}
	
	public void stop() {
		System.out.println("Stop !");
	}
	
	public void addFules(int f) {
		cfsize += f ;
	}

}
```

##### 객체간의 관계

- 객체 지향 프로그램에서는 객체는 다른 객체와 관계를 맺음.
- 관계의 종류
  - 집합 관계 : 완성품 - 부품
  - 사용 관계 : 완성품 - 사용자
  - 상속 관계 : (하위) 완성품 - (상위) 종류

