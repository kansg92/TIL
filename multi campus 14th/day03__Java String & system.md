# **📢 day03\_\_Java String & 제어문**

전체적으로 기본적인 자바 프로그래밍 실행 과정과 기초적인 것부터 디테일하게 설명하면서 강의가 진행되었다. 처음에는 지루해서 집중이 되진 않았지만 3일차부터 어느정도 강의에 적응이 되었는지 조금씩 집중하는 시간도 길어지고 기초적인 부분이 부족한것도 동시 많이 느껴 집중도가 높은 강의가 되었다.

## **📌 수업 정리 내용**

### 💡자바 프로그래밍 실행 과정.

```java
package day03;

public class P90 {

	public static void main(String[] args) {
		// Primitive type
		int a = 10;
		int b = 10;
		int c = a + b ;
		// Reference type
		String s = "ABC";
		System.out.println(s);
		System.out.println(c);
	}
}
```

#### 🔍 **Primitive type**

1. 실행버튼이 눌리면 Memory에 자바 메모리공간 생성됨
2. 자바 메모리 공간안에는 CODE, STACK, HEAP라는 영역이 생김.
3. CODE영역에 HDD(또는SSD)안에 들어 있는 CLASS파일 P90 이 들어가게됨.
4. 10이란 값(우항 값)은 STACK 이라는 영역에 들어가게됨
5. 변수 a(좌항 값)도 STACK영역으로 들어가는데 그릇과 같은 모형임. 즉 int a라는 그릇에 10이 담김
6. 순차적으로 b도 위와 같은 일을 반복함.
7. a + b 라는 연산은 CPU로 넘어가서 처리가 된후 STACK으로 넘어가고, 'c' 의 그릇에 담김.
8. "c"를 출력하라는 명령과 함께 c가 시스템에 출력되고. 코드실행이 종료됨. 종료됨과 동시에 자바영역 메모리는 삭제됨.

#### 🔍 **Reference type**

1. Reference type같은 경우에는 STACK이 아닌 HEAP영역으로 들어가게 된다.
2. HEAP영역에서 STACK영역으로 옮겨지고 값형태가아닌 HEAP의 주소(메모리의 위치정보)로서 들어간다.
3. HEAP메모리는 실행이 끝나면 지워지지 않지만, 자바는 이런 메모리를 자동적으로 지워준다.

### **💡 String(문자열)**

- 변수란, 하나의 값을 저장할 수 있는 메모리 공간.
- ' ' 작은 따옴표는 character, " " 큰 따옴표는 String을 담을 수 있다.
- String(Refernece type) 데이터의 특징.

```java
		String s1 = "abc";
		String s2 = "abc";
		if(s1 == s2) { // 주소(reference)를 비교하는것.
			System.out.println("Equals Reference ..");
		}
		if (s1.equals(s2)) { // String 안의 값(value)을 비교하는것
			System.out.println("Equals String..");
		}
		String s1 = "ABC";
		String s2 = new String("ABC"); // String의 새로운 HEAP's 데이터인 주소를 만듦
		String s3 = "ABC";
		String s4 = new String("ABC"); // String의 새로운 HEAP's 데이터인 주소를 만듦

		if (s1 == s2) {
			System.out.println("Equals Reference");
		}else {
			System.out.println("Not equals refernece");
		}// 결과값 : Not equals refernece

		if (s1 == s3) {
			System.out.println("Equals Reference");
		}else {
			System.out.println("Not equals refernece");
		}// 결과값 : Equals Reference

		if (s1.equals(s2)) {
			System.out.println("Equals String");
		}else {
			System.out.println("Not equals String");
		}// 결과값 : Equals String
```

### **💡 Java의 제어문**

- 정상적인 코드 실행 흐름 - ,main() 메소드의 시작인 중괄호 ( 에서 끝 중괄호 }까지 위 -> 아래 방향으로 실행.
- 제어문은 조건문(if , switch), 반복문(for, while)이 있다.
- if하나로도 프로그램을 짤 수 있다. 굳이 else를 쓰지 않아도 되는 경우가 있다.
