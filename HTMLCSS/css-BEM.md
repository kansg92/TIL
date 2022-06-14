# CSS 방법론, BEM 구조



## BEM 기본 구조

- BEM은 Block, Element, Modifier를 뜻하며, CSS 방법론 중 하나이다. CSS 방법론이란 CSS 클래스네임을 어떻게 지으면 좋을지에대한 고민을 하는 것 이다.

- BEM은 기본적으로 ID를 사용하지않으며, class만을 사용한다.
- '어떻게 보이는가' 가 아닌 **'어떤 목적인가'** 에 따라 이름을 짓는다.
- 예를 들어, 에러 메시지를 띄우는 p태그에는 `.red` 가 아닌 `.error`라는 이름을 줘야한다.
- 이름을 연결할 때는 `block-name`과 같이 하이픈 하나만 써서 연결한다.



## Block / Element / Modifier



### (1) Block

- 재사용 가능한 기능적응로 독립전인 페이지 컴포넌트를 블럭이라고 부른다.
- 즉 하나의 객체로 분리하여 다른곳에서 쓸 수 있는 단위를 말한다.
- 블럭은 블럭을 감쌀 수 있다. (`.header > .logo` 는 header라는 블럭안에 logo라는 블럭이 들어간 형태이다.)



### (2) Element

- 엘리먼트는 블럭을 구성하는 단위이다.
- 블럭은 독립적인 형태인 반면, 엘리먼트는 의존적인 형태이다.
- 자신이 속한 블럭 내에서만 의미를 가지기 때문에 블럭안에서 떼어다 다른데 쓸 수 없다.

```html
	
<form class="search-form">
    <input class="search-form__input"/>
    <button class="search-form__button">Search</button>
</form>
```

- 위 예시에서 `.search-form` 은 블럭이고 `search-form__input`과 `search-form__button`은 엘리먼트이다.
- 엘리먼트 또한 중첩이 가능하다. `.block > .block__element1 > .block__element2` 도 가능하다.
- BEM의 특징은 `.block__element1 > ` 를 `.block__element2` 의 하위 엘리먼트를 보지 않고 둘다 똑같이 `.block`의 엘리먼트로 취급한다는 점이 같다.
- 따라서 클래스네임에 캐스케이딩을 여러번 표시할 필요가 없다.



#### BEM의 옳바르지 않는 예

```html
<form class="search-form">
	<div class="search-form__content" >
		<input class="search-form__content__input" />
		<button class="search-form__content__button">Search</button>
	</div>
</form>
```

#### BEM의 옳바른 예.

```html
<form class="search-form">
	<div class="search-form__content" >
		<input class="search-form__input" />
		<button class="search-form__button">Search</button>
	</div>
</form>
```



### (3) Modifier

- Modifier는 **블럭이나 엘리먼트의 속성**을 담당한다. 생긴게 조금 다르거나, 다르게 동작하는 블럭이나 엘리먼트를 만들 때 사용하면 된다.

#### Modifier - boolean Type

```html
<ul class="tab">
	<li class="tab__item tab__item--focused">탭 01</li>
	<li class="tab__item">탭 02</li>
	<li class="tab__item">탭 03</li>
</ul>
```

- 위 코든에서 `--focused`가 수식어에 해당한다. 저렇게 작성된 코드는 `boolean type`이라고 하는데 그 값이 **true** 라고 가정하고 사용한다.

#### Modifier - Key-Value Type

```html
<div class="column">
	<strong class="title">일반 로그인</strong>
	<form class="form-login form-login--theme-normal">
		 <input type="text" class="form-login__id" />
		 <input type="password" class="form-login__password" />
	</form>
</div>
<div class="column">
	<strong class="title tile--color-gray">VIP 로그인 (준비중)</strong>
	<form class="form-login form-login--theme-special form-login--disalbed">
		 <input type="text" class="form-login__id" />
		 <input type="password" class="form-login__password" />
	</form>
</div>
```

- 위 예시에서 `color-gray`와 `theme-normal`은 `key-value` 타입에 해당한다.



## 사용예시 - HTML

```html
<!--
  [출처]
  http://uyeong.github.io/bem-style-mdn/
-->

<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.2/css/all.css" integrity="sha384-fnmOCqbTlWIlj8LyTjo7mOUStjsKC4pOpQbqyi7RrhN7udi9RwhKkMHpvLbHG9Sr" crossorigin="anonymous">

<div class="header">
  <div class="header__inner">
    <!-- tabzilla -->
    <div class="tabzilla">
      <a href="#" class="tabzilla__link">
        <span>mozilla</span>
      </a>
    </div>
    <!-- header__logo -->
    <div class="header__logo">
      <div class="logo">
        <a href="#" class="logo__link">
          <h1>MDN</h1>
        </a>
      </div>
    </div>
    <!-- header__auth -->
    <div class="header__auth header__auth--opened">
      <div class="auth">
        <div class="auth-means">
          <p class="auth-means__text">Sign in with</p>
          <ul class="auth-means__list">
            <li class="auth-means__item auth-menas__item--persona">
              <a href="#">
                <i class="fas fa-user"></i>
                <span class="blind">Persona</span>
              </a>
            </li>
            <li class="auth-means__item auth-menas__item--github">
              <a href="#">
                <i class="fab fa-github"></i>
                <span class="blind">Github</span>
              </a>
            </li>
          </ul>
        </div>
        <div class="auth-picker">
          <ul class="auth-picker__list">
            <li class="auth-picker__item">
              <a href="#">
                <i class="fas fa-user"></i>
                <span>Persona</span>
              </a>
            </li>
            <li class="auth-picker__item">
              <a href="#">
                <i class="fab fa-github"></i>
                <span>Github</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- nav -->
    <div class="nav">
      <ul class="nav__list">
        <li class="nav__item">
          <a href="#" class="nav__link">
            <span>Nav Menu 01</span>
            <i class="fa fa-caret-down"></i>
          </a>
          <!-- nav__submenu -->
          <div class="nav__submenu nav__submenu--col2">
              <div class="nav-submenu">
                <!-- nav-submenu__column -->
                <div class="nav-submenu__column">
                  <strong class="nav-submenu__title">Column 01</strong>
                  <ul class="nav-submenu__list">
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">HTML</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">CSS</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">Javascript</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">HTML</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">CSS</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">Javascript</a>
                    </li>
                  </ul>
                </div>
                <!-- nav-submenu__column -->
                <div class="nav-submenu__column">
                  <strong class="nav-submenu__title">Column 02</strong>
                  <ul class="nav-submenu__list">
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">Anne</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">NYKIM</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">Nana</a>
                    </li>
                    <li class="nav-submenu__item">
                      <a href="#" class="nav-submenu__link">...more</a>
                    </li>
                  </ul>
                </div>
                <button class="nav-submenu__close">
                  <span class="blind">Close submenu</span>
                  <i class="fa fa-times-circle"></i>
                </button>
              </div>
          </div>
        </li>
        <li class="nav__item">
          <a href="#" class="nav__link">
            <span>Nav Menu 02</span>
          </a>
        </li>
        <li class="nav__item">
          <a href="#" class="nav__link">
            <span>Nav Menu 03</span>
          </a>
        </li>
        <li class="nav__item">
          <a href="#" class="nav__link">
            <span>Nav Menu 04</span>
          </a>
        </li>
      </ul>
    </div>
    <!-- header__search -->
    <div class="header__search">
      <div class="search">
        <form>
          <div class="search__inner">
            <div class="search__title">
              <label for="main-search">
                <i class="fa fa-search"></i>
                <span class="blind">Search</span>
              </label>
            </div>
            <input type="text" id="main-search" class="search__input search__input--extend"> <!--focus시 .search__input--extend 클래스를
            추가합니다-->
            <input type="submit" class="search__button blind" value="Search">
          </div>
        </form>
      </div>
    </div>
  </div>
</div>

<h2>search를 별도 분리한 경우</h2>
<div class="search">
  <form>
    <div class="search__inner">
      <div class="search__title">
        <label for="main-search">
          <i class="fa fa-search"></i>
          <span class="blind">Search</span>
        </label>
      </div>
      <input type="text" id="main-search" class="search__input "> <!--focus시 .search__input--extend 클래스를
추가합니다-->
      <input type="submit" class="search__button blind" value="Search">
    </div>
  </form>
</div>
```





## 사용예시 -CSS

```css
// ================
// _common.scss
// ================

* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
  box-sizing: border-box;
}

.blind {
  display: none;
}

body {
  background-color: #fafafa;
}


// ================
// _header.scss
// ================

.header {
  width: 100%;
  background-color: #eaeff2;
  
  &__inner {
    position: relative;
    width: 100%;
    max-width: 1200px;
    min-width: 800px;
    height: 120px;
    margin: 0 auto;
    padding: 0 20px;
  }
  
  &__logo {
    margin-bottom: 30px;
  }
  
  &__auth {
    position: absolute;
    top: 20px;
    right: 180px;

    &--opened {
      .auth-means {
        border-radius: 8px 8px 0 0;
      }
      .auth-picker {
        display: block;
      }
    }
  }
  
  &__search {
    position: absolute;
    top: 60px;
    right: 0;
    
    .search__input {
      width: 60px;
    
      &[class$=--extend] {
        width: 160px;
      }
    }
  }
}


.nav {
  
  &__list {
    display: flex;
  }
  
  &__item {
    position: relative;
    margin-left: 40px;
    
    &:first-child {
      margin-left: 0;
    }
  }
  
  &__link {
    color: #4d4e53;
    font-size: 18px;
    font-weight: bold;
    text-transform: uppercase;
    
    &:hover {
      text-decoration: underline;
    }
  }
  
  &__submenu {
    position: absolute;
    top: 34px;
    left: 0;
    z-index: 10;
  }
}

.nav-submenu {
  display: none;
  background: #fff;
  border-top: 6px solid #333;
  box-shadow: 3px 4px 10px #eaeaea;
  
  [class$=--col2] &{
    display: flex;
  }
  
  &__column {
    min-width: 140px;
    padding: 10px 0;
    border-left: 1px solid #ccc;
    
    &:first-child {
      border-left: 0;
    }
  }
  
  &__title {
    display: block;
    margin: 10px 0;
    text-align: center;
  }
  
  &__link {
    display: block;
    padding: 0 12px;
    margin: 4px;
    font-size: 14px;
    color: #0095dd;
    
    &:hover {
      text-decoration: underline;
    }
  }

  &__close {
    position: absolute;
    top: 10px;
    right: 4px;
    background: transparent;
    border: 0;
    cursor: pointer;
  }
}

.search {
  &__inner {
    position: relative;
  }
  &__title {
    position: absolute;
    top: 4px;
    right: 4px;
    font-size: 12px;
  }
  &__input {
    width: 100%;
    border: 0;
    border-radius: 3px;
    padding: 4px;
  }
}

// ================
// _partial.scss
// ================

.tabzilla {
  position: absolute;
  top: 10px;
  right: 40px;
  
  &__link {
    font-size: 20px;
    color: #333;
    text-decoration: none;
    font-weight: bold;
  }
}

.logo {
  width: 153px;
  height: 55px;
  background-color: #aaa;
  
  &__link {
    color: #fff;
    text-decoration: none;
    text-align: center;
    line-height: 52px;
  }
}

.auth {
  
  &-means {
    display: flex;
    background-color: #ccc;
    border-radius: 8px;
    padding: 4px 6px;
    
    &__text {
      margin-right: 4px;
      line-height: 160%;
      color: #333;
      font-size: 14px;
    }
    
    &__list {
      display: flex;
    }
    
    &__item {
      width: 24px;
      height: 24px;
      margin: 0 3px;
      
      a {
        display: block;
        width: 100%;
        height: 100%;
        padding: 2px 6px;
        border-radius: 4px;
        font-size: 13px;
        color: #fff;
      }
      
      &[class$=--persona] a{
        background: linear-gradient(#43a6e2,#1d80bc);
      }
      
      &[class$=--github] a {
        background: linear-gradient(#5d649a,#40456a);
      }
    }
  } //end of .auth-means
  
  &-picker {
    display: none;
    
    &__list {
      position: relative;
      z-index: 1;
    }
    
    &__item {
      a {
        display: block;
        color: #0095dd;
        padding: 4px;
        background: #fff;
        
        &:hover {
          background-color: #e0e0e0;
          
          span {
            text-decoration: underline;
          }
        }
      }
    }
    
    &__item:last-child a {
      border-radius: 0 0 8px 8px;
    }
  }
}
```



### BEM 장점

1. 클래스네임으로만 마크업 구조를 알 수 있다.
2. SASS의 부보참조자(&)를 사용에 최적화가 되어 있다.
3. 작성된 SASS의 요소를 쉽게 찾을 수 있다.
   1. `.header` 아래 `&__logo`,`&__search`로 작성하기 때문에 직관적으로 알 수 있다.
4. SASS 작성 시, 늘어지는 셀렉팅을 막아준다.
   1. 기존에 nested 방식으로 SASS를 작성하면, 컴파일 시 셀렉팅도 끝도 없이 길어지는 경우가 있다.
   2. BEM방식을  쓰면 너도 나도 엘리먼트라서 굳이 깊에 nested할 필요가 없어진다.

```html
<!-- 자료 출저 nykim.work/15 -->

/*기존에 쓰던 방식*/
.header {
   .nav {
      position: absolute;
      .list {
         list-style: none;
      }
      .item {
         /*너무 길어진다 싶을 때만 밖으로(근본없는 들여쓰기!)*/
         outline: 0;
         .link {
            color: red;
         }
      }
   }
}
 
/*BEM*/
.header {
   &__nav {
      position: absolute;
   }
   &__list {
      clor: red;
   }
   &__item {
      /*여기 있는 모든 요소들은 블럭 내의 엘리먼트이기 때문에 캐스케이딩과 무관하게 병렬 작성*/
      outline: 0;
   }
   &__link {
      color: red;
   }
}

```

5. 디자인 - 마크업 - 프론트엔드 간의 의사소통이 활발하고, 마크업 단계부터 구조를 탄탄하게 짜야한다면 BEM을 많이 쓰인다.



### 단점

1. 클래스 네임이 너무 길어진다. 명확히 클래스명을 해주어야하기때문에 클래스네임이 과도하게 길어지는 경우가 있다.
2. 이에 따라 마크업이 한눈에 들어오지 않는 단점도 따라온다.
3. 특히 JS로 모디파이어를 변경해야할때 `block--name_element-name--modifier-name`처럼 길게 작성해야한다.
4. 하이픈과 언더바가 혼재되어 있어, 더블클릭해서 클래스네임을 선택할때 한번에 선택이 안되는 문제가 있다.





##### 자료 출저

https://nykim.work/15

