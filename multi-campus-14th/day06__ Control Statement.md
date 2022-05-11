# day06__제어문

#### switch문

- `if`문과 비슷한 조건문이지만 `if`문과 다르게 쓰임.

- 범위는 지정이 안됨. 어떤 경우일 경우만 가능.

- 실수의 data값은 실행이 되지않음. 실수는 x.xx000000.... 으로 가기때문 비교 불가.

- string은 가능.

- 기본형태(각 `case`마다 반드시 `break`가 있어야 멈춤. )

  - ```java
    		int a = 10;
      		switch (a) {
      		case 10:
      			System.out.println("큰수");
                break; // break가없으면 일치하여도 다음 case로넘어간다.
      		case 5 :
      			System.out.println("중간수");
                break;
      		case 1 :
      			System.out.println("작은수");
      			break;
      		default:
      			break;
      		}
    ```

- if문이 쓰기 어려울경우 사용(ex. 각 관리자마다 권한 부여가능 같은 기능 구현에 쓰임.) 

  - 		```java
      	Random r = new Random();
      	int n = r.nextInt(3)+1;
      	System.out.println(n);
      	switch (n) {
      	case 1:
      		System.out.println("냉장고");
      		break;
      	case 2:
      		System.out.println("세탁기");
      		break;
      	case 3 :
      		System.out.println("핸드폰");
      		break;
      	default:
      		break;
      	}
      ```

## 반복문

- 중괄호 블록 내용을 반복적으로 실핼할 때 사용
- 종류 : `for문` ,`while문`, do-while(거의 쓰지않음.)
- 반복문은 항상 시작과 끝이 있어야하며. 끝까지 반복을 하게된다.

### `for문`

- 기본형태 

  - ```java
    	for (int i = 0; i < 5; i++) {
    		
    	}
    ```

- 

### `while 문`

- for문과 동일한 기능이며, 변수를 밖에서 선언하는점이 for문과 다르다

- 변수가 증가된채로 변수를 사용할 수 있다.

- 기본형태

  - **주의사항** : 아래와 같을때 증가함수 `s++`이 프린트아웃 보다 위에 있을 경우 11까지 나오기 때문에 증가조건을 잘 맞추어야 한다.

  - ```java
    	int s = 1;
    	while (s <= 10) {
            system.out.println("while...." + s);
    		s++;
    	}
    ```

​	

### `if 문 + continue`

```java
	// i가 홀수 일때만 출력해라.
	for (int i = 1; i <= 10; i++) {
		if ( i % 2 == 0) {
			continue;
		}
		System.out.println("Foor Loop:" + i);
	} // 결과값 : 1, 3, 5, 7, 9
```

- 반복문 내에서만 사용되며, 반복이 진행되는 도중 continue문을 만나면 반복문의 끝으로 이동하여 다음 반복문으로 넘어간다
- 나머지가 0이 나오는 경우 continue로 넘어가서 아래 println은 출력안함.
- 상황에 따라 리소스를 많이 가져갈수도, 적게 가져갈수도 있다.