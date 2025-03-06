# REACT



## CREATE REACT APP

1 . 사전에 nodeJS를 설치해야함!

```node
1. npx 입력 ( vs code 에서 node로 터미널 접속)
2. npx create-react-app 어플리케이션이름
3. npm start 하면 리액트 실행됨.
4.  npm i prop-types  prop-types 설치
5. 
```



## CSS 모듈화

1. CSS 파일 생성

   ```
   .title{
       font-family: Arial, Helvetica, sans-serif;
       font-size: 18px;
   }
   ```

2.  사용하는 곳에 import

   ```
   function App() {
     return (
       <div className="App">
         <h1 className ={styles.title}>Welcome back!</h1>
         <Button text={"Continue"}/>
       </div>
     );
   }
   ```

3. class 는 랜덤한 이름을 가지게된다.

   ![image-20230513083835140](C:\Users\kan\AppData\Roaming\Typora\typora-user-images\image-20230513083835140.png)

   

