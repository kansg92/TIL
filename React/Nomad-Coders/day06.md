# REACT



## EFFECTS



### use EFFECTS

1. 우리 코드가 딱 한번만 실행될 수 있도록 보호해주는 기능.
2. 첫번째 argument : 딱 한번만 실행하고 싶은 코드
3. 두전빼 argument :  해당 변수가 변화 할 때 함수를 실행되는 아규먼트

```react
All imports in import declaration are unused.ts(6192)
(alias) function useEffect(effect: EffectCallback, deps?: DependencyList): void
import useEffect
Accepts a function that contains imperative, possibly effectful code.

@param effect — Imperative function that can return a cleanup function

@param deps — If present, effect will only activate if the values in the list change.

@version — 16.8.0

@see — https://react.dev/reference/react/useEffect
```



```react
import { useState, useEffect } from "react";

function App() {
  const [counter, setValue] = useState(0);
  const onClick = () => setValue((prev) => prev + 1);
  console.log("i run all the time");	--> render 될 때마다 호출됨
  const iRunOnlyOnce = () => {
    console.log("i run only once");		--> 오로지 처음 render 될 떄마다 호출됨
  };
  useEffect(iRunOnlyOnce, []);
  return (
    <div className="App">
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
```





### Clean up

1. 컴포넌트가 destroy 될 때 발생
2. 처음생성될때는 return 전 함수가 실행, 컴포넌트가 destroy 될 때 return 함수가 실행됨.

```react
import { useState, useEffect } from "react";

function Hello() {
  useEffect(() => {
    console.log("I'm here! :)");			   --> Hello 함수(컴포넌트)가 실행될 때 발생
    return () => console.log("Bye Bye... :("); --> Hello 컴포넌트가 사라질때 실행됨
  }, []);
  return <h1>Hello</h1>;
}

function App() {
  const [showing, setShowing] = useState(false);
  const onClick = () => setShowing((prev) => !prev);
  return (
    <div>
      {showing ? <Hello /> : null}
      <button onClick={onClick}>{showing ? "hide" : "Show"}</button>
    </div>
  );
}

export default App;
```





```react
import { useState, useEffect } from "react";

function Hello() {
  function byeFn(){
    console.log("Bye..... :(");
  }
  function hiFn (){
    console.log("I'm here! :)");
    return byeFn;
  }
  useEffect(hiFn, []);
  return <h1>Hello</h1>;
}

function App() {
  const [showing, setShowing] = useState(false);
  const onClick = () => setShowing((prev) => !prev);
  return (
    <div>
      {showing ? <Hello /> : null}
      <button onClick={onClick}>{showing ? "hide" : "Show"}</button>
    </div>
  );
}

export default App;
```

