# 📢day26__thymleat,boottrap 사용



## HTML 반응형웹



- 반응형웹을 만들기위에서는 `head`태그에 `meta`태그를 추가한다.



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
스크린크기에따라 색 변경.
```





웹을 구성하는데 있어서 `.jsp` or `thymleaf` 를 통해 구성이 가능하다.



```html
thymleaf
xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)"

<section th:include="${center} ? ${center} : maincenter"></section>
th:include="${scenter} ? ${scenter} : @{home/homemain}"
```



day04 - .jsp 

day044 - thymleaf

- xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)"

day045 - 044 조금더 복잡하게

day046 - bootstrap활용.



#### bootstrap 활용

