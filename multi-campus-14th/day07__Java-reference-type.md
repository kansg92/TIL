# ๐ขday07__Java reference type

#### `outter`

- ์๋ฐ์์๋ง ๋์ค๋ ํน์ง for๋ฌธ์์ ์ฐ์ด๋ฉฐ, break๋ฅผ ํ๊ณ  ์ธ๋ถ for๋ฌธ๋ ๊ฐ์ด break๋ฅผ ๋ง๋๋ ๊ฒ.

  

```java
	outter:
	for (int i = 2; i < 10; i++) {
		if (i%2 == 1 ) {
			continue;
		}
		System.out.println(i + " ๋จ ์์ --------");
		for (int j = 1; j < 10; j++) {
			if ( i * j == 28) {
				break outter;
			}
			System.out.printf("%d * %d = %d \n", i,j,(i*j));
		}
	}
```

- 28์ด ๋์ค๋ฉด ์ ์ฒด ํจ์๊ฐ ๋ฉ์ถ๊ฒ ๋๋ค.

## ์ฐธ์กฐํ์( reference type)

- ๊ธฐ๋ณธํ์(primitive type) : ์ ์, ์ค์, ๋ฌธ์, ๋ผ๋ฆฌ
- ์ฐธ์กฐํ์(reference type) : ๋ฐฐ์ด, ์ด๊ฑฐ, ํด๋์ค, ์ธํฐํ์ด์ค
- ๊ธฐ๋ณธ ํ์์ ์ค์  ๊ฐ์ ๋ณ์ ์์ ์ ์ฅํ์ง๋ง, ์ฐธ์กฐ ํ์์ ๋ฐฐ์ด, ์ด๊ฑฐ, ํด๋์ค, ์ธํฐํ์ด์ค๋ฅผ ์ด์ฉํด์ ์ ์ธ๋ ๋ณ์๋ ๋ฉ๋ชจ๋ฆฌ์ ์ฃผ์๋ฅผ ๊ฐ์ผ๋ก ๊ฐ๋๋ค.
- ์ฆ, ์ฃผ์๋ฅผ ํตํด ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ๋ค๋ ๋ป์์ ์ฐธ์กฐ ํ์์ด๋ผ๊ณ  ๋ถ๋ฅธ๋ค.
- ์ฐธ์กฐํ์์ ํ ์์ญ์ ์ฃผ์๋ฅผ ์์ฑํ๊ณ  ๊ฐ ๊ฐ์ ์คํ ์์ญ์ ์์ด๊ฒ ๋๋ค.

### ๋ฉ๋ชจ๋ฆฌ ์ฌ์ฉ ์์ญ

![image-20220412130827134](day07__.assets/image-20220412130827134-16497365137131.png)

[^์ฐธ์กฐ]:  ์ด๊ฒ์ด ์๋ฐ๋ค / ์ ์ฉ๊ถ ์ง์ p140



### reference type ์ ์ฐ์ฐ

#### `==`, `!=` ์ฐ์ฐ

- ์ฐธ์กฐํ์์ ๋์ผํ ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ๋์ง, ๋ค๋ฅธ ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ๋์ง ์์๋ณผ ๋ ์ฌ์ฉ. 

- ์ฆ, ํ์์ญ์ ๊ฐ์ฒด(์ฃผ์)๊ฐ ๋์ผํ์ง ํ์ธํ๋ ์ฐ์ฐ์ด๋ฉฐ ๊ฐ์ ๊ฐ์๋ ์ฃผ์๊ฐ ๋ค๋ฅด๋ฉด ๋ค๋ฅด๊ฒ ๋์จ๋ค.

  

### reference type ์ ๋ถ๋ฅ

#### (1) null type

- ํ ์์ญ์ ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ์ง ์๋๋ค๋ ๋ป.
- null๊ฐ์ด ๋์ ๋๋ฉด ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ์ง ์๋ ๋ฏ.
- null๊ฐ๋ ์ด๊ธฐ๊ฐ์ผ๋ก ์ฌ์ฉํ  ์ ์์ผ๋ฉฐ, ์ด๊ธฐํ๋ ์ฐธ์กฐ ๋ณ์๋ ํ ๋น ์ํ๋ก ์คํ ์์ญ์ ์์ฑ ๋๋ค.
- ์์ธ๊ฐ ๋ฐ์๋ ๊ณณ์์ ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ์ง ์์ ์ํ๋ก ์ฐธ์กฐ ํ์ ๋ณ์๋ฅผ ์ฌ์ฉ ํ๊ณ  ์์์ ์์์ผํ๋ค.
- NullPointerException์ ๊ฐ์ฅ ๋ง์ด ๋ณผ ์ ์๋ ์์ธ ์ค ํ๋์ด๋ค.

#### (2) String type

- ๋ฌธ์์ด์ ์ง์  ๋ณ์์ ์ ์ฅ๋๋ ๊ฒ์ฒ๋ผ ๋ณด์ด์ง๋ง ๊ทธ๋ ์ง ์๋ค.
- ๋ฌธ์์ด์ `String` ๊ฐ์ฒด๋ก ์์ฑ๋๊ณ  ๋ณ์๋ `String` ๊ฐ์ฒด๋ฅผ ์ฐธ์กฐํ๋ค.
- `new` ์ฐ์ฐ์๋ฅผ ์ฌ์ฉํ๋ฉด ์๋ก์ด ํ ์์ญ์ ์์ฑ ๋๊ธฐ ๋๋ฌธ์ ๊ฐ์ ๊ฐ์ ๊ฐ์ง๋๋ผ๋ ๋ค๋ฅด๋ค. ์๋ s1 ์ s2 ๋ ๊ฐ์ ๋ณด์ด์ง๋ง ํ ์์ญ์ด ๋ฌ๋ผ `s1==s2` ๋ `false`๋ฅผ ํ ํด๋ธ๋ค.

```java
	String s1 = "abc";
	String s2 = new String("abc");
```

- ์ฃผ์์ ๊ฐ๊ณผ ์๊ด์์ด ๋น๊ตํ๊ธฐ ์ํด์๋ ๊ฐ์ฒด์ `equals()`๋ฉ์๋๋ฅผ ์ฌ์ฉํด์ผ ํ๋ค. `equals()`๋งค์๋๋ ๋งค๊ฐ๊ฐ์ผ๋ก ์ฃผ์ด์ง ๋น๊ต ๋ฌธ์์ด์ด ๋์ผํ์ง ๋น๊ตํ ํ `true`, `false`๋ฅผ ๋ฆฌํดํ๋ค.
- ์ฐธ์กฐ๋ฅผ ์์ String ๊ฐ์ฒด๋ ์ฐ๋ ๊ธฐ ๊ฐ์ฒด๋ก ์ทจ๊ธํ๊ณ  ๋ฉ๋ชจ๋ฆฌ์์ ์๋ ์ ๊ฑฐ๋๋ค.

#### (3) Array type

- ๋ฐฐ์ด์ ๊ฐ์ ํ์์ ๋ฐ์ดํฐ๋ฅผ ์ฐ์๋ ๊ณต๊ฐ์ ๋์ด์ํค๊ณ , ๊ฐ ๋ฐ์ดํฐ์ ์ธ๋ฑ์ค๋ฅผ ๋ถ์ฌํด ๋์ ์๋ฃ ๊ตฌ์กฐ์ด๋ค.
- ๋ฐฐ์ด์ ๊ฐ์ ํ์์ ๋ฐ์ดํฐ๋ง ์ ์ฅํ  ์ ์๋ค. (int๋ฐฐ์ด์ int๋ง String๋ฐฐ์ด์ String๋ง)
- ํ ๋ฒ ์์ฑ๋ ๋ฐฐ์ด์ ๊ธธ์ด๋ฅผ ๋๋ฆฌ๊ฑฐ๋ ์ค์ผ ์ ์๋ค.
- ๋ฐฐ์ด ๋ณ์๋ null๊ฐ์ผ๋ก ์ด๊ธฐํ ๋  ์ ์๋ค.
- ๋ฐฐ์ด์ ์ฃผ์๊ฐ STACK ์์ญ์ ์ ์ฅ๋๊ณ  ๋ฐฐ์ด์ ๊ฐ ๊ฐ์ฒด๋ HEAP์์ญ์ ์ ์ฅ ๋๋ค.
- String๋ฐฐ์ด ๊ฐ์ ๊ฒฝ์ฐ์๋ HEAP์์ญ ์์ ๊ฐ ๋ฐฐ์ด ๊ณต๊ฐ์ ๊ฐ์ฒด ๊ฐ์ ์ฐธ์กฐํ๋ค.

```java
	int ar [] = new int[4]; // ๊ฐ์ฒด๊ฐ 4๊ฐ์ธ int ๋ฐฐ์ด ์์ฑ.
	ar[0] = 0;
	ar[1] = 1;
	ar[2] = 2;
	ar[3] = 3;
// int ar [] = {0,1,2,3} ๊ณผ ๊ฐ์ ํํ๋ก๋ ๊ฐ๋ฅํ๋ค.

	System.out.println(ar); //์ฃผ์๊ฐ์ด ์ฐํ๋ค.	:[I@626b2d4a
	System.out.println(Arrays.toString(ar)); // ๋ฐฐ์ด์ ๋ชจ๋  ๊ฐ์ฒด๋ฅผ ์ถ๋ ฅ. :[0, 1, 2, 3]
	for (int i = 0; i < ar.length; i++) {
		System.out.println(ar[i]); // ๊ฐ ๋ฐฐ์ด์ ๊ฐ ์ถ๋ ฅ. ; 0, 1, 2, 3
	}
```

##### ๋ค์ฐจ์ ๋ฐฐ์ด

- 2์ฐจ์ ๋ฐฐ์ด์ ํ๋ ฌ๊ณผ ๊ฐ์ด ํ๊ณผ ์ด๋ก์ ๊ตฌ์ฑ๋ ๋ฐฐ์ด์ ๋งํ๋ค.

  ```java
  	int ar [][] = new int [3][];
  	ar[0] = new int[3];
  	ar[1] = new int[3];
  	ar[2] = new int[3];
  // int ar [][] = new int[3][3]; ๊ณผ ๊ฐ๋ค.
  ```

- 