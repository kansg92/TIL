# React



## Props

1. 컴포넌트에 사용 되는 변수 인자를 말한다.
2. props를 사용 하려면 함수에서 props의 변수나 함수를 선언 해주어야 사용이 가능하다. 
3. 함수에 들어가는 인자로서 리액트에서 함수에 유일하게 들어가는 인자이다.
4. 오브젝트 형태를 띈다.
5. App에서 정의한 오브젝트의 값을 변수로 사용이 가능하다.
6. function functionName(props){} 
7. function functionName({arg1, arg2, arg3 = "13"}) 형태로도 사용 가능하며 default값을 설정해 줄 수 있다.



### 사용 형태 1

```react
  <script type="text/babel">
    // functuon 의 props(objec형태임)는 오로지 하나의 인자만 들어 갈 수 있다.
    // props.banana -> App에서 정의한 인자 값이 들어간다.
    function Btn(props) {
      return (
        <button
          style={{
            backgroundColor: "coral",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
          }}
        >
          {props.banana}  // 하단의 정의한 banana를 사용함.
        </button>
      );
    }
    function App() {
      return (
        <div>
          <Btn banana="Save Changes" x="props인자" /> 
          <Btn banana="Continue" y="props인자" />
        </div>
      );
    }

    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
```



### 사용 형태 2

```react
  <script type="text/babel">
    // functuon 의 props(objec형태임)는 오로지 하나의 인자만 들어 갈 수 있다.
    // props.banana -> App에서 정의한 인자 값이 들어간다.
    function Btn({banana, big}) {
      return (
        <button
          style={{
            backgroundColor: "coral",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
            fontSize : big ? 18 : 16,
          }}
        >
          {banana}  
        </button>
      );
    }
    function App() {
      return (
        <div>
          <Btn banana="Save Changes" big={true} /> 
          <Btn banana="Continue" big={false} />
        </div>
      );
    }

    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
  
```



### Props 함수 사용

```react
    function Btn({ banana, changeValue }) {
      return (
        <button
          onClick={changeValue}     --> changevalue onclcik 하면 발생되도록 설정.
          style={{
            backgroundColor: "coral",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
          }}
        >
          {banana}
        </button>
      );
    }
    function App() {
      const [value, setValue] = React.useState("Save Changes"); 
      const changeValue = () => setValue("Revert Changes"); // 2. 부모상태(state)의 값을 변경함.
      return (
        <div>
          <Btn banana={value} changeValue={changeValue} />  // 3. changevalue props추가하여 사용.
          <Btn banana="Continue" />
        </div>
      );
    }
```



### *******MEMO*******

1. 부모의 상태가 변경되는 것만 변경 되도록 한다.
2. 변경되지 않는 props는 reRender 되지 않기 때문에 데이터의 이점이 있을 것 같다. 

```react
    function Btn({ banana, changeValue }) {
      console.log(text, "was rendered")
      return (
          <button
            onClick={changeValue}
            style={{
              backgroundColor: "coral",
              color: "white",
              padding: "10px 20px",
              border: 0,
              borderRadius: 10,
            }}
          >
            {banana}
          </button>
      );
    }
    const MemorizedBtn = React.memo(Btn);  // Btn 컴포넌트를 memo 함...
    function App() {
      const [value, setValue] = React.useState("Save Changes");
      const changeValue = () => setValue("Revert Changes");			// props가 변경되지 않으면 rerender하지 않음
      return (
        <div>
          <MemorizedBtn banana={value} changeValue={changeValue} />
          <MemorizedBtn banana="Continue" />
        </div>
      );
    }
```



### Props Type

1. https://unpkg.com/prop-types@15.7.2/prop-types.js 적용..
2. prop의 타입을 명시하여서 코드 에러를 줄여줌
3. 해당 라이브러리를 설치하면 콘솔창에서 proptype을 타이핑하면 어떤 type들이 있는지 알 수 있다.
4. type이 맞지 않는 다면 에러를 만들어줌
5. .isRequired를 통해 필수 값을 지정해 줄 수 있음.



#### 아래와 같이 사용 가능.

``` react
<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script> --> 스크립트 추가
	function Btn({ banana, changeValue, fontSize = 13 }) { 
      console.log(banana, "was rendered");
      return (
        <button
          onClick={changeValue}
          style={{
            backgroundColor: "coral",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
            fontSize: fontSize,
          }}
        >
          {banana}
        </button>
      );
    }
    Btn.protoTypes = {
      banana : PropTypes.string.isRequired,
      fontSize : PropTypes.number.isRequired,
    }ㄱ
```

