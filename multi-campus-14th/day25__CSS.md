# 📢day25__HTML2 & CSS



## HTML

### block 과 INLINE

- block : 전체 가로줄을 차지하는 요소 태그

  - ```html
    <address>, <article>, <aside>, <blockgquote>, <canvas>, <dd>, <div>, <dl>, <hr>, <header>, <form>,<h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <table>, <pre>, <ul>, <p>, <ol>, <video>
    ```

- inline : 해당 컨텐츠만 차지하는 요소 태그

  - ```html
    <a>, <i>, <span>, <abbr>, <img>, <strong>, <b>, <input>, <sub>, <br>, <code>, <em>, <small>, <tt>, <map>, <textarea>, <label>, <sup>, <q>, <button>, <cite>
    ```



### `<div></div>` 태그

- 블록 형태의 기본적인 태그로 분할할때 사용한다.

​		

## CSS

### id

- HTML에서 유일무이한 이름을 갖는것으로 해당 1개의 이름만 css적용.

### class

- HTML 태그에 이름을 부여하고 해당 이름의 class는 모두 css적용.

### 속성 선택자(form에서 사용.)

```css
	input[type="text"]{
		background-color:green;
	}
	input[type="submit"]:hover{
        background-color:green;
        color:coral;
	}

```



### 폰트 적용하기.

[구글 무료폰트 사이트](https://fonts.google.com/)

- 폰트에서 추가
- css파일에 import하기 (복사붙이기)
- fontfamily 통해서 적용 (복사붙이기)