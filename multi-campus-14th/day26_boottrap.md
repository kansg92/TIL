# ๐ขday26__thymleat,boottrap ์ฌ์ฉ



## HTML ๋ฐ์ํ์น



- ๋ฐ์ํ์น์ ๋ง๋ค๊ธฐ์์์๋ `head`ํ๊ทธ์ `meta`ํ๊ทธ๋ฅผ ์ถ๊ฐํ๋ค.



#### HTML

```html
<meta name = "viewport" content="user-scalable=no,initial-scale=1,maximum-scale=1">
```



#### CSS

```css
	@media screen and (max-width: 767px){
		body {
			background:coral;
		}
	}
	@media screen and (min-width: 767px) and (max-width: 959px){
		body {
			background:green;
		}
	}
	@media screen and (min-width: 960px){
		body {
			background:white;
		}
	}
์คํฌ๋ฆฐํฌ๊ธฐ์๋ฐ๋ผ ์ ๋ณ๊ฒฝ.
```





์น์ ๊ตฌ์ฑํ๋๋ฐ ์์ด์ `.jsp` or `thymleaf` ๋ฅผ ํตํด ๊ตฌ์ฑ์ด ๊ฐ๋ฅํ๋ค.



```html
thymleaf
xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)"

<section th:include="${center} ? ${center} : maincenter"></section>
th:include="${scenter} ? ${scenter} : @{home/homemain}"
```



day04 - .jsp 

day044 - thymleaf

- xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)"

day045 - 044 ์กฐ๊ธ๋ ๋ณต์กํ๊ฒ

day046 - bootstrapํ์ฉ.



#### bootstrap ํ์ฉ

