# 📢day08\_\_Java workshop

## Guess number game

```java
public static void main(String[] args) {
	// Number Guess Game
	// 1 ~ 99 랜덤숫자중 한개의 숫자를 받든다.
	// 숫자를 입력하고 해당 숫자보다 낮으면 down, 높으면 up
	// 10회 이상 입력하면 Game over. 다시 도전 하세요.
	// 최종 숫자를 맞추면 시스템 종료.
	Scanner sc = new Scanner(System.in);
	Random ran = new Random();
	int randnum = 0;
	System.out.println("Game start..");
	String stdIn = "";
	while (true) {
		//예외 상황 입력시 반복.
		try {

			randnum = ran.nextInt(99)+1;
			// 리 게임 시 카운트 초기화.
			int count = 0;
			for(int i = 0; i <= 10; i++ ) {
				System.out.print("Guess number(1~99) :");
				System.out.println("");
				stdIn = sc.next();
				int num = Integer.parseInt(stdIn);
				count++;
				// 10회 입력시 게임 실패
				if ( count == 10) {
					System.out.println("Game over, 10회 이내로 맞추셔야합니다. 다시도전하세요:)");
					break;
				}
				// 입력 숫자가 높을 시 down
				if ( num > randnum ) {
					System.out.println("Down");
					continue;
				//입력 숫자가 낮을 시 up
				} else if ( num < randnum) {
					System.out.println("Up");
					continue;
				// 정답시 게임 더 진행 여부 확인.
				} else if ( num == randnum) {
					System.out.printf("정답! 축하드립니다. 도전횟수 : %d회 \n", count );
					System.out.println("게임을 이어 하시겠습니까? (input : yes or no):");
					stdIn = sc.next();
					//yes or no 만 입력 받기.
					while(true) {
						if ( !(stdIn.equals("yes") ||stdIn.equals("no") ) ) {
						System.out.println("yes or no 만입력 가능합니다. 다시입력하세요 :");
						stdIn = sc.next();
						}
						if ( stdIn.equals("yes")) {
							break;
						} else if(stdIn.equals("no")) {
							System.out.println("게임이 종료 되었습니다.");
							sc.close();
							return;
						}
					}
				}
				break;
			}
			//예외상황시 숫자 재입력.
		} catch (Exception e) {
			System.out.println("숫자만 입력해주세요.");
			continue;
		}
	}

}
```

## Lotto Game

```java
public static void main(String[] args) {
	// Lotto Game
	// 로또 숫자를 입력 받는다. 6자리.
	// 서로다른 숫자를 입력하고 번호확인!
	Scanner sc = new Scanner(System.in);
	Random r = new Random();

	// 1. 6자리 배열 만들기.
	int ar [] = new int [6];
	int user [] = new int [6];

	// 2. 로또 번호 생성.(1~45)
	for (int i = 0; i < ar.length; i++) {
		ar [i] = r.nextInt(45)+1;
		// 중복 수 제거.
		for (int j = 0; j < i ; j++) {
			if (ar[i] == ar[j] ) {
				i--;
			}
		}
	}
	//3. 번호 입력.

	for (int i = 0; i < ar.length; i++) {
		// 예외상황 방지.
		try {
			System.out.println("로또 번호를 입력하세요." + (i+1) + "번:" );
			String snum = sc.next();
			int num = Integer.parseInt(snum);
			user[i] = num;
			// 숫자 범위 지정 (1~45만 입력)
			if ( num < 0 || num > 45 ) {
				System.out.println("1~45 숫자만 입력 가능합니다.");
				i--;
				continue;
			}
			// 중복 입력시 재입력.
			for (int j = 0; j < i; j++) {
				if (user[i] == user[j] ) {
					System.out.println("중복된 번호입니다 다시 입력하세요.");
					i--;
				}
			}
			// 숫자 미입력시 다시 해당 번호 입력.
		} catch (Exception e) {
			System.out.println("숫자만 입력 가능합니다.");
			i--;
			continue;
		}
	}
	//4.같은 번호인지 비교하기.
	int count = 0;
	for (int i = 0; i < ar.length; i++) {
		if(ar[i] == user [i]) {
			count++;
		}
	}
	//5. 몇 등 \인지 확인하기.
	System.out.println("당신이 입력한 로또 번호:" + Arrays.toString(user));
	System.out.println(count);
	if (count == 6) {
		System.out.println("1등 당첨");
	}else if (count == 5) {
		System.out.println("2등 당첨");
	}else if (count == 4) {
		System.out.println("3등 당첨");
	}else if (count == 3 ) {
		System.out.println("4등 당첨");
	}
	System.out.println("아쉽습니다... 다음에 도전하세요.");
	System.out.println("로또 최종 번호:" + Arrays.toString(ar));

	sc.close();

}
```

}
