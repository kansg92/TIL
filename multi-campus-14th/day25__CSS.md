# ๐ขday25__HTML2 & CSS



## HTML

### block ๊ณผ INLINE

- block : ์ ์ฒด ๊ฐ๋ก์ค์ ์ฐจ์งํ๋ ์์ ํ๊ทธ

  - ```html
    <address>, <article>, <aside>, <blockgquote>, <canvas>, <dd>, <div>, <dl>, <hr>, <header>, <form>,<h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <table>, <pre>, <ul>, <p>, <ol>, <video>
    ```

- inline : ํด๋น ์ปจํ์ธ ๋ง ์ฐจ์งํ๋ ์์ ํ๊ทธ

  - ```html
    <a>, <i>, <span>, <abbr>, <img>, <strong>, <b>, <input>, <sub>, <br>, <code>, <em>, <small>, <tt>, <map>, <textarea>, <label>, <sup>, <q>, <button>, <cite>
    ```



### `<div></div>` ํ๊ทธ

- ๋ธ๋ก ํํ์ ๊ธฐ๋ณธ์ ์ธ ํ๊ทธ๋ก ๋ถํ ํ ๋ ์ฌ์ฉํ๋ค.

โ		

## CSS

### id

- HTML์์ ์ ์ผ๋ฌด์ดํ ์ด๋ฆ์ ๊ฐ๋๊ฒ์ผ๋ก ํด๋น 1๊ฐ์ ์ด๋ฆ๋ง css์ ์ฉ.

### class

- HTML ํ๊ทธ์ ์ด๋ฆ์ ๋ถ์ฌํ๊ณ  ํด๋น ์ด๋ฆ์ class๋ ๋ชจ๋ css์ ์ฉ.

### ์์ฑ ์ ํ์(form์์ ์ฌ์ฉ.)

```css
	input[type="text"]{
		background-color:green;
	}
	input[type="submit"]:hover{
        background-color:green;
        color:coral;
	}

```



### ํฐํธ ์ ์ฉํ๊ธฐ.

[๊ตฌ๊ธ ๋ฌด๋ฃํฐํธ ์ฌ์ดํธ](https://fonts.google.com/)

- ํฐํธ์์ ์ถ๊ฐ
- cssํ์ผ์ importํ๊ธฐ (๋ณต์ฌ๋ถ์ด๊ธฐ)
- fontfamily ํตํด์ ์ ์ฉ (๋ณต์ฌ๋ถ์ด๊ธฐ)