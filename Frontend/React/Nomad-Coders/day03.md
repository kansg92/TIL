# React



### State

1. 일반적으로 컴포넌트의 내부에서 변경 가능한 데이터를 관리 해야할 때 사용한다.
2. 프로퍼티(props)의 특징은 내부에서 값을 바꿀수 없다. 하지만 값을 바꾸어야할 때 이럴 때 state라는 것을 사용한다.
3. 값을 저장하거나 변경할 수 있는 객체로 보통 이벤트와 함께 사용된다.
4. 컴포넌트에서 동적인 값을 상대(state)라고 부르며, 동적인 데이터를 다룰 때 사용된다.



```react
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    let counter = 0;

    function App() {
      const [amount, setAmount] = React.useState(0);
      const [flipped, setFlipped] = React.useState(true);
      const onChange = (event) => {
        setAmount(event.target.value);
      };
      function reset() {
        setAmount(0);
      }
      const onFlip = () => {
        reset();
        setFlipped((current) => !current);
        
      };
      return (
        <div>
          <h3 className="hi">Super Converter</h3>
          <div>
            <label htmlFor="minutes">minutes</label>
            <input
            value={flipped ? amount : amount * 60}
              id="minutes"
              placeholder="Minutes"
              type="number"
              onChange={onChange}
              disabled={!flipped}
            />
          </div>
          <div>
            <label htmlFor="hours">hours</label>
            <input
              value={!flipped ? amount : Math.round(amount / 60)}
              id="hours"
              placeholder="Hours"
              type="number"
              disabled={flipped}
              onChange={onChange}
            />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onFlip}>Flip</button>
        </div>
      );
    }
    ReactDOM.render(<App />, root);
  </script>
```





```react
<script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    let counter = 0;

    function MinutesToHours() {
      const [amount, setAmount] = React.useState(0);
      const [flipped, setFlipped] = React.useState(true);
      const onChange = (event) => {
        setAmount(event.target.value);
      };
      function reset() {
        setAmount(0);
      }
      const onFlip = () => {
        reset();
        setFlipped((current) => !current);
      };
      return (
        <div>
          <div>
            <label htmlFor="minutes">minutes</label>
            <input
              value={flipped ? amount : amount * 60}
              id="minutes"
              placeholder="Minutes"
              type="number"
              onChange={onChange}
              disabled={!flipped}
            />
          </div>
          <div>
            <label htmlFor="hours">hours</label>
            <input
              value={!flipped ? amount : Math.round(amount / 60 * 10) /10}
              id="hours"
              placeholder="Hours"
              type="number"
              disabled={flipped}
              onChange={onChange}
            />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onFlip}>Flip</button>
        </div>
      );
    }
    function KmToMiles() {
      const [amount, setAmount] = React.useState(0);
      const [flipped, setFlipped] = React.useState(true);
      const onChange = (event) => {
        setAmount(event.target.value);
      };
      function reset() {
        setAmount(0);
      }
      const onFlip = () => {
        reset();
        setFlipped((current) => !current);
      };
      return (
        <div>
          <div>
            <label htmlFor="Km">Km</label>
            <input
              value={flipped ? amount : amount / 0.621371}
              id="Km"
              placeholder="Km"
              type="number"
              onChange={onChange}
              disabled={!flipped}
            />
          </div>
          <div>
            <label htmlFor="Miles">Miles</label>
            <input
              value={!flipped ? amount : amount * 0.621371}
              id="Miles"
              placeholder="Miles"
              type="number"
              disabled={flipped}
              onChange={onChange}
            />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onFlip}>Flip</button>
        </div>
      );
    }

    function App() {
      const [index, setIndex] = React.useState("0");
      const onSelect = (event) => {
        setIndex(event.target.value);
      };
      return (
        <div>
          <h3 className="hi">Super Converter</h3>
          <select value={index} onChange={onSelect}>
            <option value="0">Minutes & Hours</option>
            <option value="1">Km & Miles</option>
          </select>
          <hr />
          {index === "0" ? <MinutesToHours /> : null}
          {index === "1" ? <KmToMiles /> : null}
        </div>
      );
    }

    ReactDOM.render(<App />, root);
  </script>
```

