# ๐ขday24__HTML

HTML ์ ํ๊ทธ๋ค๋ก ๊ตฌ์ฑ๋์ด์ง๋ค.

`head`๋ `html`์ ์์ฑ, `body`ํ๊ทธ๋ ๋ด์ฉ์๋ณด์ฌ์ค๋ค.

### HTML ํ๊ทธ ์ข๋ฅ

1. `<h1></h1>` ํ๊ทธ : ๊ตต๊ณ  ํฐ ๊ธ์์ธ๋ ์ฌ์ฉ ๋ณดํต ํค๋๊ฐ์๊ณณ์ ์ฐ์ด๋ฉฐ `h1 ~ h6` ๊น์ง ์์ผ๋ฉฐ ์ซ์๊ฐ ํด์๋ก ์์์ง.

2. `<p></p>` ํ๊ทธ :  ๊ธฐ๋ณธ์ ์ธ ๊ธ์ ์ธ ๋ ์ฐ๋ ํ๊ทธ

3. `<a href = "http://www..."></a>` ํ๊ทธ : ๋งํฌ๋ฅผ ์ฐ๊ฒฐํ๋ ํ๊ทธ. 
   - `<a href="#"></a>` ํ๊ทธ : ๋งํฌ๊ธฐ๋ฅ์ ์ฌ์ฉํ์ง ์์๋ ์. ๋ณดํต ํ๋ก๊ทธ๋จ๊ณผ ์ฐ๋ํ์ฌ ๋งํฌ๋ฅผ ์ฌ์ฉํ ๋ ์ฐ์ธ๋ค.
4. `<ul></ul>` ,` <ol></ol>` ํ๊ทธ : ๋ฆฌ์คํธ์ ํ๊ทธ ๋ด๋ถ์ `<li></li>` ํ๊ทธ๋ฅผ ๋ฃ์ด ์ฌ์ฉํ๊ธฐ๋ํจ.` ol`ํ๊ทธ๋  ๋๋ฒ๋ง๋์ด ์์๋จ.
5. `<table></table>` ํ๊ทธ : table์ ์์ฑํ ๋ ์ฐ๋ ํ๊ทธ. ๋ค์๊ณผ๊ฐ์ํํ.

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

6. `<img src ="img๊ฒฝ๋ก">` ํ๊ทธ : ์ด๋ฏธ์ง ํ๊ทธ.
7. `<br>` ํ๊ทธ : blockํํ ํ๊ทธ๋ค ์ฌ์ด ์ค๋๊ธฐ๊ธฐ ํ๊ทธ.
8. `<form></form>` ํ๊ทธ : formํํ๋ฅผ ๋ง๋ค๋ ์ฐ๋ ํ๊ทธ. ์๋ฒ์ ์ฐ๋์ ํ๊ธฐ์ํด ํ์ฉ๋์ด์ง๋ค.
   - ์น์๋ฒ์ ์น๋ธ๋ผ์ฐ์  ์ฐ๋ํ๋๋ฐ ์์ด ๋ฐฉ๋ฒ์ ํฌ๊ฒ `get` ๋ฐฉ์๊ณผ `post` ๋ฐฉ์์ด ์กด์ฌํ๋ค.
     - get = ๋ชจ๋  ์ ๋ณด๊ฐ ๋ธ๋ผ์ฐ์  ๋ธ์ถ๋๋ฉฐ ๋ณด์์ ์ข์ง ๋ชปํ๋ค.
     - `post`๋ฐฉ์ : ๋ชจ๋  ์ ๋ณด๊ฐ ๋ธ๋ผ์ฐ์ ์ ๋ธ์ถ๋์ง ์๋๋ค.

```html
<form>
    ID<input type="text" name="id"><br>
    PWD<input type="password" name="pwd"><br>
    AGE<input type="number" name="age"><br>
    sumbit<input type="submit" value="registar" >
</form>
```

9. `formํ๊ทธ  ์ค <input>` ํ๊ทธ

```html
<form action="register2" method="post">
    <fieldset>
        <legend>ํ์๊ฐ์</legend>
        ID<input type="text" name="id"><br>
        PWD<input type="password" name="pwd"><br>
        AGE<input type="number" name="age"><br>
        BIRTH<input type="date" name="birth"><br>
        GENDER<br>
        <!-- radio : n๊ฐ์ค 1๊ฐ๋ง ์ ํ ๊ฐ๋ฅ.(๋ง์ฐ์ค ์ฒดํฌํตํด์) ๋ค์ค์ ํX -->
        <input type="radio" name="gender" value="f">Female<br>
        <input type="radio" name="gender" value="m">Male<br>
        <input type="radio" name="gender" value="a">Aje<br>
        HOBBY<br>
        <!-- checkbox : n๊ฐ์ค n๊ฐ ์ ํ ๊ฐ๋ฅ.(๋ง์ฐ์ค ์ฒดํฌํตํด์) ๋ค์ค์ ํO -->			
        <input type="checkbox" name="hobby" value="s">Study<br>
        <input type="checkbox" name="hobby" value="t">Train<br>
        <input type="checkbox" name="hobby" value="e">Eat<br>
        Car<br>
        <!-- select : ์ต์์ค 1๊ฐ ์ ํ ๊ฐ๋ฅ  -->
        <select name="car">
            <option value="k3">k3</option>
            <option value="k5">k5</option>
            <option value="k7">k7</option>
        </select><br>
        Resume<br>
        <textarea name="resume" rows="10" cols="100"></textarea><br>
        <!-- hidden : ํ๋ฉด์ ๋ณด์ด์ง ์๋๊ฒ.  -->
        <input type="hidden" name="loginid" value="kan"><br>
        <!-- range : ๋ฒ์ ๋ฐ๋ฅผ ๋ง๋ค์ด์ค.  -->
        <input type="range" name="range" size="10" step="1">
    </fieldset>
    <!-- submit : ์๋ฒ๋ก ๋ณด๋ด๊ธฐ..  -->
    <input type="submit" value="REGISTER">
    <!-- reset : ์์ฑ๋ ๋ด์ฉ ๋ชจ๋ ์ง์ฐ๊ธฐ.  -->
    <input type="reset" value="RESET">
</form>
```







###### ์ถ๊ฐ์ ์ผ๋ก ๊ณต๋ถํ ๊ฒ.

1. Spring ๊ฐ๋.
2. jsp ์ HTML ์ฐจ์ด, ๊ฐ๋.
