# 🎁Parameter 와 Argument

---

#### 공부목적

공부를 하다보니 함수안에있는 변수를 어떨때는 파라미터 어떨때는 아규먼트라고 말을하는데 정확히 그 뜻을 이해 못하고 쫓아갔는데 확실히 할 필요가 있을거 같다. 공부해보니 둘은 서로 비슷하면서 다르다. 이제는 서로를 구분해서 정확히 명칭하고 전달하는 습관을 가져야한다.

---



### Parameter(매개변수)

- Parameter, 우리말로 번역하면 **"매개변수"**라고 한다.
- 함수의 정의부분에 나열되는 변수를 말한다.
- 즉 변수를 말한다.

```javascript
function add (param1 ,param2 ){
	param1 + param2
} // param1, param2 는 parameter
```



### Argument(전달인자)

- argument, 우리말로 번역하면 **"전달인자"**라고 한다
- 함수를 호출할 때 전달되는 실제 값을 의미한다.
- 즉, 값을 말한다.

```javascript
add(3, 5); // 3,5 는 argument
```

