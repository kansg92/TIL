# ๐ขday08\_\_Java workshop

## Guess number game

```java
public static void main(String[] args) {
	// Number Guess Game
	// 1 ~ 99 ๋๋ค์ซ์์ค ํ๊ฐ์ ์ซ์๋ฅผ ๋ฐ๋ ๋ค.
	// ์ซ์๋ฅผ ์๋ ฅํ๊ณ  ํด๋น ์ซ์๋ณด๋ค ๋ฎ์ผ๋ฉด down, ๋์ผ๋ฉด up
	// 10ํ ์ด์ ์๋ ฅํ๋ฉด Game over. ๋ค์ ๋์  ํ์ธ์.
	// ์ต์ข ์ซ์๋ฅผ ๋ง์ถ๋ฉด ์์คํ ์ข๋ฃ.
	Scanner sc = new Scanner(System.in);
	Random ran = new Random();
	int randnum = 0;
	System.out.println("Game start..");
	String stdIn = "";
	while (true) {
		//์์ธ ์ํฉ ์๋ ฅ์ ๋ฐ๋ณต.
		try {

			randnum = ran.nextInt(99)+1;
			// ๋ฆฌ ๊ฒ์ ์ ์นด์ดํธ ์ด๊ธฐํ.
			int count = 0;
			for(int i = 0; i <= 10; i++ ) {
				System.out.print("Guess number(1~99) :");
				System.out.println("");
				stdIn = sc.next();
				int num = Integer.parseInt(stdIn);
				count++;
				// 10ํ ์๋ ฅ์ ๊ฒ์ ์คํจ
				if ( count == 10) {
					System.out.println("Game over, 10ํ ์ด๋ด๋ก ๋ง์ถ์์ผํฉ๋๋ค. ๋ค์๋์ ํ์ธ์:)");
					break;
				}
				// ์๋ ฅ ์ซ์๊ฐ ๋์ ์ down
				if ( num > randnum ) {
					System.out.println("Down");
					continue;
				//์๋ ฅ ์ซ์๊ฐ ๋ฎ์ ์ up
				} else if ( num < randnum) {
					System.out.println("Up");
					continue;
				// ์ ๋ต์ ๊ฒ์ ๋ ์งํ ์ฌ๋ถ ํ์ธ.
				} else if ( num == randnum) {
					System.out.printf("์ ๋ต! ์ถํ๋๋ฆฝ๋๋ค. ๋์ ํ์ : %dํ \n", count );
					System.out.println("๊ฒ์์ ์ด์ด ํ์๊ฒ ์ต๋๊น? (input : yes or no):");
					stdIn = sc.next();
					//yes or no ๋ง ์๋ ฅ ๋ฐ๊ธฐ.
					while(true) {
						if ( !(stdIn.equals("yes") ||stdIn.equals("no") ) ) {
						System.out.println("yes or no ๋ง์๋ ฅ ๊ฐ๋ฅํฉ๋๋ค. ๋ค์์๋ ฅํ์ธ์ :");
						stdIn = sc.next();
						}
						if ( stdIn.equals("yes")) {
							break;
						} else if(stdIn.equals("no")) {
							System.out.println("๊ฒ์์ด ์ข๋ฃ ๋์์ต๋๋ค.");
							sc.close();
							return;
						}
					}
				}
				break;
			}
			//์์ธ์ํฉ์ ์ซ์ ์ฌ์๋ ฅ.
		} catch (Exception e) {
			System.out.println("์ซ์๋ง ์๋ ฅํด์ฃผ์ธ์.");
			continue;
		}
	}

}
```

## Lotto Game

```java
public static void main(String[] args) {
	// Lotto Game
	// ๋ก๋ ์ซ์๋ฅผ ์๋ ฅ ๋ฐ๋๋ค. 6์๋ฆฌ.
	// ์๋ก๋ค๋ฅธ ์ซ์๋ฅผ ์๋ ฅํ๊ณ  ๋ฒํธํ์ธ!
	Scanner sc = new Scanner(System.in);
	Random r = new Random();

	// 1. 6์๋ฆฌ ๋ฐฐ์ด ๋ง๋ค๊ธฐ.
	int ar [] = new int [6];
	int user [] = new int [6];

	// 2. ๋ก๋ ๋ฒํธ ์์ฑ.(1~45)
	for (int i = 0; i < ar.length; i++) {
		ar [i] = r.nextInt(45)+1;
		// ์ค๋ณต ์ ์ ๊ฑฐ.
		for (int j = 0; j < i ; j++) {
			if (ar[i] == ar[j] ) {
				i--;
			}
		}
	}
	//3. ๋ฒํธ ์๋ ฅ.

	for (int i = 0; i < ar.length; i++) {
		// ์์ธ์ํฉ ๋ฐฉ์ง.
		try {
			System.out.println("๋ก๋ ๋ฒํธ๋ฅผ ์๋ ฅํ์ธ์." + (i+1) + "๋ฒ:" );
			String snum = sc.next();
			int num = Integer.parseInt(snum);
			user[i] = num;
			// ์ซ์ ๋ฒ์ ์ง์  (1~45๋ง ์๋ ฅ)
			if ( num < 0 || num > 45 ) {
				System.out.println("1~45 ์ซ์๋ง ์๋ ฅ ๊ฐ๋ฅํฉ๋๋ค.");
				i--;
				continue;
			}
			// ์ค๋ณต ์๋ ฅ์ ์ฌ์๋ ฅ.
			for (int j = 0; j < i; j++) {
				if (user[i] == user[j] ) {
					System.out.println("์ค๋ณต๋ ๋ฒํธ์๋๋ค ๋ค์ ์๋ ฅํ์ธ์.");
					i--;
				}
			}
			// ์ซ์ ๋ฏธ์๋ ฅ์ ๋ค์ ํด๋น ๋ฒํธ ์๋ ฅ.
		} catch (Exception e) {
			System.out.println("์ซ์๋ง ์๋ ฅ ๊ฐ๋ฅํฉ๋๋ค.");
			i--;
			continue;
		}
	}
	//4.๊ฐ์ ๋ฒํธ์ธ์ง ๋น๊ตํ๊ธฐ.
	int count = 0;
	for (int i = 0; i < ar.length; i++) {
		if(ar[i] == user [i]) {
			count++;
		}
	}
	//5. ๋ช ๋ฑ \์ธ์ง ํ์ธํ๊ธฐ.
	System.out.println("๋น์ ์ด ์๋ ฅํ ๋ก๋ ๋ฒํธ:" + Arrays.toString(user));
	System.out.println(count);
	if (count == 6) {
		System.out.println("1๋ฑ ๋น์ฒจ");
	}else if (count == 5) {
		System.out.println("2๋ฑ ๋น์ฒจ");
	}else if (count == 4) {
		System.out.println("3๋ฑ ๋น์ฒจ");
	}else if (count == 3 ) {
		System.out.println("4๋ฑ ๋น์ฒจ");
	}
	System.out.println("์์ฝ์ต๋๋ค... ๋ค์์ ๋์ ํ์ธ์.");
	System.out.println("๋ก๋ ์ต์ข ๋ฒํธ:" + Arrays.toString(ar));

	sc.close();

}
```

}
