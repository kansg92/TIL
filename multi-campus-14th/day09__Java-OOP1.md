# π’day09__Java class

### κ°μ²΄ μ§ν₯ νλ‘κ·Έλλ°(Object Oriented Programming) 

#### OOPκ°λ

- μκ΅¬μ¬ν­μ μ -> OOAD -> OOP

- OOAD(Obecjt Oriented Analysis and Desigin) κ°λμμ μΆλ°νμκ³ , UML (Unified Modeling Language)μμ μλ°μ μ΄ λμλ€. ν΄λΉ κ°λμ JAVAμμ κ΅¬ννλ©΄μ OOP(Object Oriented Programming)κ°λμ λ§λ€μλ€.

[OOAD κ°λ](https://soniacomp.medium.com/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%A0%81-%EB%B6%84%EC%84%9D%EA%B3%BC-%EB%94%94%EC%9E%90%EC%9D%B8-object-oriented-analysis-and-design-%EC%86%8C%EA%B0%9C-part-1-%EB%B2%88%EC%97%AD-67ff58fd26c9)

[UML κ°λ](https://www.microsoft.com/ko-kr/microsoft-365/business-insights-ideas/resources/guide-to-uml-diagramming-and-database-modeling)

- OOPλ λΆνμ ν΄λΉνλ κ°μ²΄λ€μ λ¨Όμ  λ§λ€κ³ , μ΄κ²λ€μ νλμ© μ‘°λ¦½ν΄μ μμ±λ νλ‘κ·Έλ¨μ λ§λλ κΈ°λ²μ λ§νλ€.

- κ°μ²΄μ§ν₯μΈμ΄ λμ μΆμ² : [ν€λ νΌμ€νΈ λμμΈ ν¨ν΄ - νλΉλ―Έλμ΄](https://book.naver.com/bookdb/book_detail.naver?bid=22236366)

#### OOP νΉμ§

- Encapsulcation
  - κ°μ²΄μ νλ, λ©μλλ₯Ό νλλ‘ λ¬Άκ³ , μ€μ  κ΅¬ν λ΄μ©μ κ°μΆλ κ²μ λ§νλ€.
  - μΈλΆ κ°μ²΄λ κ°μ²΄ λ΄λΆμ κ΅¬μ‘°λ₯Ό μμ§ λͺ»νλ©° κ°μ²΄κ° λΈμΆν΄μ μ κ³΅νλ νλμ λ©μλλ§ μ΄μ©ν  μ μλ€.
  - νλμ λ©μλλ₯Ό μΊ‘μν νμ¬ λ³΄νΈνλ μ΄μ λ μΈλΆμ μλͺ»λ μ¬μ©μΌλ‘ μΈν΄ κ°μ²΄κ° μμλμ§ μλλ‘ νλλ° μλ€.
  - [μΊ‘μνλ λ¬΄μμΈκ°?](https://javacpro.tistory.com/31)
- Inheritance
  - μμ
- Polymorpism
  - λ€νμ±
- Abstraction
  - μΆμν

#### κ°μ²΄(Object)λ?

- λ¬Όλ¦¬μ μΌλ‘ μ‘΄μ¬νκ±°λ(μλμ°¨, μ¬λ, μ± λ±) μΆμμ μΌλ‘ μκ°ν  μ μλ κ²(νμ¬, λ μ§, κ³μ’ λ±) μ€ μμ μ μμ±μ κ°μ§κ³  μκ³  λ€λ₯Έ κ²κ³Ό μλ³ κ°λ₯ν κ²μ λ§νλ€.
- μλ°μ κ°μ²΄λ νλ(μμ±)κ³Ό λ©μλ(λμ)λ‘ κ΅¬μ±λμ΄ μλ€.
- νμ€μΈκ³μ κ°μ²΄λ₯Ό μννΈμ¨μ΄ κ°μ²΄λ‘ μ€κ³νλ κ²μ κ°μ²΄ λͺ¨λΈλ§(Object Modeling)μ΄λΌκ³  νλ€.
-  Object Modelingμ νμ€ μΈκ³ κ°μ²΄μ μμ±κ³Ό λμμ μΆλ¬λ΄μ΄ μννΈμ¨μ΄ κ°μ²΄μ νλμ λ©μλλ‘ μ ν¬νλ κ³Όμ μ΄λΌ λ³Ό μ μλ€.

##### μλμ°¨μ Object Modling

```java
// μλμ°¨ κ°μ²΄
public class Car { 
	// Attribute (μμ±, νλ)
	String name;
	String color;
	int size;
	int fsize;
	int cfsize;

	//Constructor(μμ±μ): μμ±μμ μ΄λ¦μ Classμ΄λ¦κ³Ό κ°μμΌνλ€.
	public Car() {
		this.name = "k3";
		this.color = "white";
		this.size = 1000;
		this.fsize = 50;
		this.cfsize = 0;
	}        

	// Operation (λμ, λ§€μλ)
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

##### κ°μ²΄κ°μ κ΄κ³

- κ°μ²΄ μ§ν₯ νλ‘κ·Έλ¨μμλ κ°μ²΄λ λ€λ₯Έ κ°μ²΄μ κ΄κ³λ₯Ό λ§Ίμ.
- κ΄κ³μ μ’λ₯
  - μ§ν© κ΄κ³ : μμ±ν - λΆν
  - μ¬μ© κ΄κ³ : μμ±ν - μ¬μ©μ
  - μμ κ΄κ³ : (νμ) μμ±ν - (μμ) μ’λ₯

