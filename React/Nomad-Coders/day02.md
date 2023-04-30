# React



1. 리액트에서는 HTML코드를 짜지않고 Js코드로만 작성한다.





### JSX(JavaScript XML)

``` https://unpkg.com/@babel/standalone/babel.min.js
https://unpkg.com/@babel/standalone/babel.min.js
```

- 리액트 코드를 조금더 직관적으로 바꾸어준다.
- 자바스크립트의 확장 문법이다.
- UI가 어떻게 생겨야 하는지 설명하기 위해 React와 함께 사용할 것을 권장한다.

```react
<html lang="en">
  <head> </head>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    function Title() {
      return (
        <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
          Hello I'm a Title
        </h3>
      );
    }
    const Button = () => (
      <button
        style={{ backgroundColor: "tomato" }}
        onClick={() => console.log("i'm Clicked!!")}
      >
        Click me
      </button>
    );
    /*
       1. 컴포넌트의 첫글자는 반드시 대문자여야 한다.(직접만든 요소들은..) 
       2. html요소는 소문자로 작성..
       3. <컴포넌트 /> 해당 요소로 사용하려면 선언을 할때 함수로 선언을 해주어야 컴포넌트로 사용이 가능하다!
    */ 
    const container = (
      <div>
        <Title />  
        <Button />
      </div>
    );
    ReactDOM.render(container, root);
  </script>
</html>
```

1. 리액트에서 생성되는 컴포넌트의 첫글자는 대문자로 시작해야한다.
2. HTML의 엘리먼트와 구분되기위해서 컴포넌트의 첫글자는 항상 대문자여야 한다.
3. 리액트에서 엘리먼먼트 요소로 사용하려면 선언할 때 함수 형태로 선언해주어야 한다...



### JSX 란?

- React에서는 본질적으로 렌더링 로직이 UI 로직(이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등)과 연결된다는 사실을 받아들입니다.

- React는 별도의 파일에 마크업과 로직을 넣어 *기술*을 인위적으로 분리하는 대신, 둘 다 포함하는 “컴포넌트”라고 부르는 느슨하게 연결된 유닛으로 [*관심사*를 분리](https://en.wikipedia.org/wiki/Separation_of_concerns)합니다. 이후 섹션에서 다시 컴포넌트로 돌아오겠지만, JS에 마크업을 넣는 게 익숙해지지 않는다면 [이 이야기](https://www.youtube.com/watch?v=x7cQ3mrcKaY)가 확신을 줄 것입니다.

- React는 JSX [사용이 필수가 아니지만](https://ko.legacy.reactjs.org/docs/react-without-jsx.html), 대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다. 또한 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해줍니다.



### JS와 ReactJS의 차이점

- 리액트가 아닌 경우, 일반 자바스크립트를 사용한 브라우저는 노드정보가 바뀔때마다 노드트리를 처음부터 다시 생성함.
- 5단계에 걸처서 노드 트리를 다시 생성함에 반해 리액트는 가상돔을 사용함으로써 우리 시야에서 보이는 부분만 수정해서 보여주고 모든 업데이트가 끝나면 일괄로 합쳐서 실제 돔에 던저줌.
- 프론트엔드에서는 이러한 랜더트리 단계를 얼머나 최적화 하는지가 가장 중요하다고 볼 수 있다.



#### 공부해야 할 내용

1. 노드정보란 무엇인가??
2. 노드트리란 무엇인가?
3. 브라우저의 작동원리는 무엇인가?
4. 렌더트리란 무엇인가?

### State











1. 