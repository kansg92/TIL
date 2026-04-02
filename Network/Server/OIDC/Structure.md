# OIDC flask 서버 구축

### Phase 1

최소 동작 서버

- login
- authorize
- token
- userinfo
- well-known
- jwks

### Phase 2

토큰 발급/검증 서비스 분리

- token_service
- auth_service 정도

### Phase 3

키/JWT 유틸 분리

- keys.py
- jwt_helper.py

### Phase 4

저장소 분리

- authorization code store
- token store

### Phase 5

OIDC 보강

- nonce
- PKCE
- client 검증 강화
- redirect_uri 검증 강화
- exp/ttl 정교화

### Phase 6

실사용 보강

- DB 저장소
- ERP 세션 연동
- 로그/에러 처리
- 운영 설정 분리