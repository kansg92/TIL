# ๐ขday27__javascript



## JavaScript

### Javascript์ ํ์ ๋ฐฐ๊ฒฝ๊ณผ ๋ฐ์ .

- Netscape ์ฌ๊ฐ 1996๋ 2์ ์๋ฐ์ธ์ด๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ํ์ฌ ์น ๋ธ๋ผ์ฐ์ ์์ ์คํํ๋ ์คํธ๋ฆฝํธ์ธ์ด๋ก ๋ฐํ๋์๋ค.
- HTML์ ์ ์ ์ธ ๋ถ๋ถ์ JavaScript๋ฅผ ์ด์ฉํ์ฌ ๋ค์ด๋๋ฏนํ UI์ ์ด๋ฒคํธ๋ฅผ ์ฒ๋ฆฌ์ ์ฌ์ฉ๋๋ฉฐ ์ฌ๋ฌ ๋ธ๋ผ์ฐ์  ์์ฒด๋ค์ด ๋ฒค๋์ ํนํ๋ ์คํฌ๋ฆฝํธ๋ก ๋ฐ์  ํ๊ธฐ ์์ ํ๋ค.
- ๋ชจ๋ฐ์ผ์น ๋ฐ ๋ค์ํ ์น ๊ฐ๋ฐ ๋ถ์ผ์์ ๋จ์ Livrary๋ก ์ฌ์ฉ๋๋ JavaScirpt๋ Angular JS์ ๊ฐ์ ํ๋ ์์ํฌ๋ก ๋ฐ์  ๋๋ฉฐ ์ธ๊ณ์์ ๊ฐ์ฅ ๋ง์ด ์ฌ์ฉ๋๋ ์ธ์ด๋ก ๋ฐ์  ํ๊ฒ ๋๋ค.
- OOP๋ฅผ ์ง์ํจ์ผ๋ก์ ๊ธฐ์กด์ ์คํฌ๋ฆฝํธ ์ธ์ด์ ํ๊ณ๋ฅผ ๊ทน๋ณต.
- 2005๋ AJAX๋ฅผ ๋ฐํ ํ๋ฉด์ ๋น๋๊ธฐ ํ๋ก๊ทธ๋๋ฐ ๊ฐ๋ฅํ๋๋ก ๋ฐ์ 
- 2006๋ JQuery์ ๋ฐํ๋ก ํฌ๋ก๊ทธ ๋ธ๋ผ์ฐ์ง์ด ๊ฐ๋ฅํ ์คํฌ๋ฆฝํธ ์ธ์ด๋ก ๋ฐ์ 
- 2009๋ Node.js๋ฅผ ํตํด ์๋ฒ ์ฌ์ด๋์ ์คํฌ๋ฆฝํธํ
- 2014๋ ๊ตฌ๊ธ์ Angular JS ๋ฐํ๋ฅผ ํตํ Framework๊ธฐ๋ฐ ๊ฐ๋ฐ ํ๊ฒฝ ๊ฐ๋ฐ ๊ตฌ์ถ



### JavaScript์ ํ์์ฑ

- HTML ๋ด๋ถ Contest๋ฅผ ์์ ๋กญ๊ฒ ๋ณ๊ฒฝ ์ถ๊ฐ๊ฐ ๊ฐ๋ฅํ๋ค.
- CSS๋ฅผ ์์ ๋กญ๊ฒ ๋ณ๊ฒฝ ๊ฐ๋ฅํ๋ค.
- Event๋ฅผ ์ฒ๋ฆฌ Vaildation.
  - JavaScript๋ฅผ ํตํด ํ๋ฉด์ ์๋ จ๋ ๋ฐ์ดํฐ์ ๊ฒ์  ์์ ๊ฐ๋ฅ
  - ํ๋ฉด์์ ์ด๋ฒคํธ ์ฒ๋ฆฌ ๋ฐ ์ด๋ฒคํธ์ ํ์๋ฅผ ์ ์ด ๊ฐ๋ฅ
- Web Page์์์ ํ๋ก๊ทธ๋จ ๋ถ๋ถ์ ๋ด๋นํ๋ค.
  - ๋ค์ํ API๋ฅผ ์ ๊ณตํ๊ณ  HTML5์์์ ํ๋ก๊ทธ๋จ ๋ถ๋ถ์ ๋ด๋นํ๋ค.

### JavaScript Datatype

- JavaScript์์ ๋ณ์ ์ ์ธ์ const,let,var ์ด 3๊ฐ์ง๋ก ํ  ์ ์์ผ๋ฉฐ var์ ์ฝ๋์ ์ค์ผ์ด ์๊ธธ ์ ์์ด ์ง์ํ๋ค.
  - const : ์ฌ์ ์ธ, ์ฌํ ๋น ๊ธ์ง
  - let : ์ฌ์ธ์ธ ๊ธ์ง, ์ฌํ ๋น ๊ฐ๋ฅ
  - var : ์ฌ์ ์ธ, ์ฌํ ๋น ๊ฐ๋ฅ.

```javascript
// undefined
var data1;

//number ์ ์,์ค์ ๊ตฌ๋ถ์์
var num1 = 100;
var num2 = 200.123;

//String ๋ฌธ์์ด charcter ๋ชจ๋ ํฌํจ.
var str1 = 'abc';
var str2 = "abc";

// boolean
var b = true;

//object
var obj1 = {
    id : 'id01',
    pwd : 'pwd01',
    name : 'ํ์ผ๋'
};

//array
var arr = [1,2,"srt",{'a':1}];

//function
var func = function(){
    return 100;
}
// javascript์์๋ ํจ์์์ ํจ์๋ฅผ ๋ฃ์ ์ ์๋ค.
function c(){
    return function(){
        return 100;
    };

};

let r1 = c();
let result2 = r1();
alert(result2); // return 100

function d(f){

};

let dd = function(){
    return 100;		
};
const result3 = d(dd);
alert(result3); // return 100
```

- #### [Javascript ๊ณต์ ๋ฌธ์](https://developer.mozilla.org/ko/docs/Web/JavaScript)

### JSON

- JavaScript Object Notation์ ์ฝ์์ด๋ค.
- ๊ฒฝ๋ ํ์์ผ๋ก ๋ฐ์ดํฐ๋ค์ ์์คํ ๊ฐ ์ ์กํ๋๋ฐ ์ฌ์ฉ๋๋ค.
- JavaScript์์ ํด์๊ณผ ๋ฐ์ดํฐ์ถ์ถ์ด ํธ๋ฆฌํ๋ค.
- JSONํํ ๋ฐ์ดํฐ

```json
{"employees":[
    {"firstName":"John","lastName":"Doe"},
    {"firstName":"Anna","lastName":"Smith"},
    {"firstName":"Peter","lastName":"Jones"}
]}
```



### DOM(Document Object Model)

- W3C๋ฌธ์ ๊ฐ์ฒด ๋ชจ๋ธ๋ก์ W3C์์ ์ ์ ํ ๋ฌธ์์ด๋ค. 
- ํ๋ก๊ทธ๋จ ๋ฐ ์คํธ๋ฆฝํธ๋ฅผ ๋์ ์ผ๋ก ์ก์ธ์คํ์ฌ ๋ฌธ์์ ์ฝํ์ธ , ๊ตฌ์กฐ ๋ฐ ์คํ์ผ์ ๊ฐฑ์ฑ ํ  ์ ์๋๋ก ํ๋ซํผ ๋ฐ ์ธ์ด ์ค๋ฆฝ ์ธํฐํ์ด์ค์ด๋ค.
- HTML DOM์ ์น ๋ธ๋ผ์ฐ์ ธ๋ฅผ ์ํ ๋ฌธ์ ํ์ค์ด๋ฉฐ HTML์ ์ํ ํ๋ก๊ทธ๋จ ์ธํฐํ์ด์ค ์ด๋ค.
  - ๋ชจ๋  HTML์ tag์์๋ฅผ Object๋ผ ์นญํ๋ค.
  - ๋ชจ๋  HTML์ tag์์์ Property๋ฅผ ์ค์  ํ  ์ ์๋ค.
  - ๋ชจ๋  HTML์ tag์์๋ฅผ ๋ณ๊ฒฝ, ์ถ๊ฐ, ์ญ์ ๊ฐ ๊ฐ๋ฅ ํ๋ค
  - ๋ชจ๋  HTML์ tag์์์ Event๋ฅผ ๋ฐ์ ์ํฌ ์ ์๋ค.
  - ๋ชจ๋  HTML์ tag์์์ Contents๋ฅผ ๋ณ๊ฒฝ ํ  ์ ์๋ค.
- JavaScript๋ฅผ ํตํด HTML DOM์ ์ ๊ทผ ํ๊ณ  ์์ ๋ชจ๋  ์์์ ์งํ ํ๋ค.
- HTML DOM๊ณผ JavaScript๋ฅผ ์ด์ฉํ์ฌ ๋์  HTML์ ๋ง๋ค ์ ์๋ค.
  - javascript๋ ํ์ด์ง์ ์๋ ๋ชจ๋  HTML ์์๋ฅผ ๋ณ๊ฒฝํ  ์ ์๋ค.
  - javascript๋ ๋ชจ๋  HTML ํ์ด์ง์ ์์ฑ์ ๋ณ๊ฒฝํ  ์ ์๋ค.
  - javascript๋ ํ์ด์ง์์๋ ๋ชจ๋  CSS ์คํ์ผ์ ๋ณ๊ฒฝํ  ์ ์๋ค.
  - javascript๋ HTML ์์์ ์์ฑ์ ์ ๊ฑฐ ํ  ์ ์๋ค.
  - javascript๋ ์๋ก์ด HTML์์์ ์์ฑ์ ์ถ๊ฐ ํ  ์ ์๋ค.
  - javascript๋ ๋ชจ๋  ์ด๋ฒคํธ๋ฅผ ์ ์ด ํ  ์ ์๋ค.
  - javascript๋ ๋ชจ๋  HTML TAG์ ์ด๋ฒคํธ๋ฅผ ๋ง๋ค ์ ์๋ค.





#### DOM์ ์ข๋ฅ

1. Core DOM: ๋ชจ๋  ๋ฌธ์ ํ์์ ๋ํ ํ์ค ๋ชจ๋ธ
2. HTML DOM: HTML๋ฌธ์์ ํ์ค ๋ชจ๋ธ
   1. HTML๋ฌธ์๋ฅผ ์กฐ์ํ๊ณ  ์ ๊ทผํ๋ ํ์คํ๋ ๋ฐฉ๋ฒ์ ์ ์
   2. ๋ชจ๋  HTML์์๋ HTML DOM์ ํตํด ์ ๊ทผํ ์ ์๋ค.
3. XML DOM: XML ๋ฌธ์์ ํ์ค ๋ชจ๋ธ
   1. XML๋ฌธ์์ ์ ๊ทผํ๋ฉฐ, ๊ทธ ๋ฌธ์๋ฅผ ๋ค๋ฃจ๋ ํ์คํ๋ ๋ฐฉ๋ฒ์ ์ ์
   2. ๋ชจ๋  XML์์๋ XML DOM์ ํตํด ์ ๊ทผํ  ์ ์๋ค.



![image-20220516130704700](day27__.assets/image-20220516130704700.png)

### Finding HTML Element

- document.getElementById(" ");
- document.getElementByTagName(" ");
- document.getElementByClassName(" ");
- document.querySelector(".class #id");
- document.querySelectorAll(" ");

### Changing HTML Element

- element.innerHTML =   : element ์ ๋ถ์ ๋ด์ฉ์ ๋ณ๊ฒฝํ๋ค. 
- element.attribute =   : ์์ฑ ๊ฐ์ ๋ณ๊ฒฝ ํ๋ค.
- element.setAttribute(attribute, value) : ์์ฑ ๊ฐ์ ๋ณ๊ฒฝ ํ๋ค.
- element.style.property = Style๋ฅผ ๋ณ๊ฒฝํ๋ค.



### BOM(Browser Object Model)

- ์๋ฐ์คํฌ๋ฆฝํธ๋ฅผ ํตํด ๋ธ๋ผ์ฐ์ ์์ ์ ๊ณต ํ๋ ๊ธฐ๋ฅ์ ์ ์ด ํ๋ ๋ฐฉ๋ฒ์ ์ ๊ณตํ๋ค.
  - window : Brower ์ฐฝ ์ ๋ณด๋ฅผ ์ฌ์ฉ ํ  ์ ์๋ค
  - screen : ํ์ฌ ์์คํ์ ํ๋ฉด ์ ๋ณด๋ฅผ ์ฌ์ฉ ํ  ์ ์๋ค.
  - location : URL์ ๋ณด๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
  - navigator : ์น ๋ธ๋ผ์ฐ์  ์ ๋ณด๋ฅผ ์ฌ์ฉ ํ  ์ ์๋ค.
  - popup : ๋ค์ํ popup box๋ฅผ ์ ๊ณต ํ๋ค.
  - timing: ๋ค์ํ Timer๋ฅผ ์ฌ์ฉ ํ  ์ ์๋ค.