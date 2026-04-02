sso로 리다이렉트

서버에서 로그인값 확인 

안되어있음 로그인페이지로 리다이랙트





DB계정검증

sso 세션생성

코드 발급

그 코드 붙여서 다시 리다이렉트...

outline은 코드확인후 토큰 요청

sso 에서 토큰 발급



1. 사용자 wiki 접속

2. Outline → SSO authorize redirect
   ```
   https://sso.zeroton.co/authorize
       ?client_id=outline
       &redirect_uri=https://wiki.zeroton.co/auth/oidc.callback
       &response_type=code
       &scope=openid profile email
       &state=XXXX
   ```

3. SSO 서버 authorize 처리

   1. client_id 확인
   2. redirect_uri 확인
   3. 로그인 세션 확인

4. 로그인 안되어있으면 로그인 페이지 리다이랙트

5. 사용자 로그인

6. 로그인 성공 세션 등록

7. authorization code  생성

8. wiki callback으로 redirect

   ```
   https://wiki.zeroton.co/auth/oidc.callback
       ?code=abc123
       &state=XXXX
   ```

9. wiki -> sso /token 요청

   ```
   POST /token
   
   BODY
   grant_type=authorization_code
   code=abc123
   client_id=outline
   client_secret=xxxx
   redirect_uri=https://wiki.zeroton.co/auth/oidc.callback
   ```

10. sso 서버 토큰 발급

    1. code 존제 체크

    2. code 만료 체크

    3. client 체크

    4. redirect_uri체크

    5. 문제 없음 JWT 발급 (`id_token`. `access_token`)

       ```
       {
        "access_token": "xxx",
        "id_token": "yyy",
        "token_type": "Bearer",
        "expires_in": 3600
       }
       ```

11. wiki  토큰 검증

12.  outline 내부 로그인 생성

