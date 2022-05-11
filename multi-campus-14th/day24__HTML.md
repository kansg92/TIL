# 📢day24__HTML

HTML 은 태그들로 구성되어진다.

`head`는 `html`의 속성, `body`태그는 내용을보여준다.

### HTML 태그 종류

1. `<h1></h1>` 태그 : 굵고 큰 글을쓸때 사용 보통 헤더같은곳에 쓰이며 `h1 ~ h6` 까지 있으며 숫자가 클수록 작아짐.

2. `<p></p>` 태그 :  기본적인 글을 쓸 때 쓰는 태그

3. `<a href = "http://www..."></a>` 태그 : 링크를 연결하는 태그. 
   - `<a href="#"></a>` 태그 : 링크기능을 사용하지 않을때 씀. 보통 프로그램과 연동하여 링크를 사용할때 쓰인다.
4. `<ul></ul>` ,` <ol></ol>` 태그 : 리스트업 태그 내부에 `<li></li>` 태그를 넣어 사용하기도함.` ol`태그는  넘버링되어 시작됨.
5. `<table></table>` 태그 : table을 작성할때 쓰는 태그. 다음과같은형태.

```html
<table >
    <thead>
        <tr><th>id</th><th>name</th><th>age</th></tr>
    </thead>
    <tbody>
        <tr><td>id01</td><td>lee</td><td>10</td></tr>
        <tr><td>id02</td><td>kim</td><td>15</td></tr>
        <tr><td>id03</td><td>park</td><td>25</td></tr>
        <tr><td>id04</td><td>hong</td><td>20</td></tr>
    </tbody>
</table>
```

6. `<img src ="img경로">` 태그 : 이미지 태그.
7. `<br>` 태그 : block형태 태그들 사이 줄넘기기 태그.
8. `<form></form>` 태그 : form형태를 만들때 쓰는 태그. 서버와 연동을 하기위해 활용되어진다.
   - 웹서버와 웹브라우저 연동하는데 있어 방법은 크게 `get` 방식과 `post` 방식이 존재한다.
     - get = 모든 정보가 브라우저 노출되며 보안상 좋지 못하다.
     - `post`방식 : 모든 정보가 브라우저에 노출되지 않는다.

```html
<form>
    ID<input type="text" name="id"><br>
    PWD<input type="password" name="pwd"><br>
    AGE<input type="number" name="age"><br>
    sumbit<input type="submit" value="registar" >
</form>
```

9. `form태그  중 <input>` 태그

```html
<form action="register2" method="post">
    <fieldset>
        <legend>회원가입</legend>
        ID<input type="text" name="id"><br>
        PWD<input type="password" name="pwd"><br>
        AGE<input type="number" name="age"><br>
        BIRTH<input type="date" name="birth"><br>
        GENDER<br>
        <!-- radio : n개중 1개만 선택 가능.(마우스 체크통해서) 다중선택X -->
        <input type="radio" name="gender" value="f">Female<br>
        <input type="radio" name="gender" value="m">Male<br>
        <input type="radio" name="gender" value="a">Aje<br>
        HOBBY<br>
        <!-- checkbox : n개중 n개 선택 가능.(마우스 체크통해서) 다중선택O -->			
        <input type="checkbox" name="hobby" value="s">Study<br>
        <input type="checkbox" name="hobby" value="t">Train<br>
        <input type="checkbox" name="hobby" value="e">Eat<br>
        Car<br>
        <!-- select : 옵션중 1개 선택 가능  -->
        <select name="car">
            <option value="k3">k3</option>
            <option value="k5">k5</option>
            <option value="k7">k7</option>
        </select><br>
        Resume<br>
        <textarea name="resume" rows="10" cols="100"></textarea><br>
        <!-- hidden : 화면상 보이지 않는것.  -->
        <input type="hidden" name="loginid" value="kan"><br>
        <!-- range : 범위 바를 만들어줌.  -->
        <input type="range" name="range" size="10" step="1">
    </fieldset>
    <!-- submit : 서버로 보내기..  -->
    <input type="submit" value="REGISTER">
    <!-- reset : 작성된 내용 모두 지우기.  -->
    <input type="reset" value="RESET">
</form>
```







###### 추가적으로 공부할것.

1. Spring 개념.
2. jsp 와 HTML 차이, 개념.
