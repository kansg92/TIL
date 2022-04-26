# 📢day13__JAVA 예외처리

### 예외와 예외 클래스

- 예외란 사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 인해 발생하는 프로그램 오류를 말한다.
- 예외가 발생되면 프로그램은 곧바로 종료된다는 점에서는 에러와 동일하다.
- 그러나 예외는 예외처리(Exception Handling)를 통해 프로그램을 종료하지 않고 정상 실행 상태가 유지되도록 할 수 있다.

#### 예외의 종류

- 일반 예외 : 컴파일러 체크 예외라고도 하며, 자바 소스를 컴파일하는 과정에서 예외 처리 코드가 필요한지 검사하기 때문에 발생 한다.   
  - 컴파일러가 체크해서 실행전 예외상황을 말해줌.
- 실행 예외 : 컴파일하는 과정에서 예외 처리 코드를 검사하지 않는 예외를 말한다.
  - 컴파일러가 실행되고 나서 예외 상황을 말해줌.
- 예외 처리 추가하면 정상 실행 상태로 돌아갈 수 있음.

#### 오류의 종류

- 하드웨어의 잘못된 동작 또는 고장으로 인한 오류
- 에러가 발생되면 프로그램 종료
- 정상 실행 상태로 돌아갈 수 없음

#### 예외 처리 코드(try-catch-finally)

```java
	Scanner sc = new Scanner(System.in);
	System.out.println("Input number");
	String num = sc.next();
	int n = 0;
	int result = 0;
	// 해당 코드실행되면
	try {
		n = Integer.parseInt(num);
		result = 100 / n ;
		System.out.println(result);
        //해당 에러를 잡아내고 실행됨.
	} catch (NumberFormatException e) {
		System.out.println("숫자가 아닙니다.");	
	} catch (ArithmeticException e) {
		System.out.println("분모가 0 입니다.");
        //에러상황 없으면 finally코드 실행.
	} finally {
		sc.close();
		System.out.println("end");
	}
		
```