# 노션 대안 정리

1. Wiki.js
2. BookStack
3. Xwiki
4. DokuWiki
5. Outline  
6. Docmost



| 이름          | 라이선스                         | LDAP 호환     | 사용성 | 파일 업로드       | 이미지 업로드 | Slack 연동          | DB / API Export 연동  | DBMS                       |
| ------------- | -------------------------------- | ------------- | ------ | ----------------- | ------------- | ------------------- | --------------------- | -------------------------- |
| **Wiki.js**   | AGPLv3 (무료)                    | 공식 지원     | ☆      | ✅                 | ✅             | ✅ 공식 Webhook      | ✅ REST / GraphQL / DB | PostgreSQL, MySQL, MariaDB |
| **BookStack** | MIT (무료)                       | 공식 지원     | ⭐⭐⭐⭐⭐  | ✅                 | ✅             | ⚠️ Webhook 직접 구성 | ✅ REST API / DB       | MySQL, MariaDB             |
| **XWiki**     | LGPL (무료)                      | 지원          | ⭐⭐⭐    | ✅                 | ✅             | ⚠️ 애드온/스크립트   | ✅ REST / 구조화 API   | MySQL, PostgreSQL, Oracle  |
| **DokuWiki**  | GPLv2 (무료)                     | 플러그인      | ⭐⭐⭐    | ✅                 | ✅             | ❌ (커스텀 필요)     | ⚠️ 파일기반 / 제한적   | ❌ DB 없음 (파일 기반)      |
| **Outline**   | BSL → OSS 전환 (무료 셀프호스팅) | SSO 경유      | ⭐⭐⭐⭐   | 외부 스토리지(S3) | 외부 스토리지 | ✅ Slack 연동 강함   | ✅ API Export          | PostgreSQL                 |
| **Docmost**   | AGPLv3 (무료)                    | ❌ (OIDC 위주) | ⭐⭐⭐⭐☆  | ✅                 | ✅             | ⚠️ 제한적            | ⚠️ API 미성숙          | PostgreSQL                 |



## ① 알림(Notification) 연동 — *기본이자 필수*

> “위키에서 무슨 일이 생기면 슬랙으로 알려준다”

### 가능한 것

- 문서 생성 / 수정 / 삭제 알림
- 특정 공간(Space) / 카테고리별 알림
- 공지사항만 전용 채널로 전송

### 실제 메시지 예

```
📢 [공지] VPN 접속 정책 변경
작성자: IT팀
👉 https://wiki.company.com/it/vpn-policy
```

### 이걸 **잘 지원하는 경우**

- **Wiki.js** ✅ (공식 Webhook)
- **Outline** ✅
- **BookStack** ⚠️ (Webhook 수동)

👉 이 단계만 돼도 **“슬랙 연동 된다”**고 말하긴 해
 하지만, **“잘 된다”**고 하려면 여기서 끝이 아님.

------

## ② 컨텍스트 링크(Context Linking)

> “슬랙에서 바로 위키로 자연스럽게 이어진다”

### 잘 된다는 기준

- 링크 미리보기 정상 표시
- 제목 / 요약 / 아이콘 자동 노출
- 권한 없는 사용자는 접근 차단

### 예

슬랙에 링크 붙이면 👇

```
📘 IT 인프라 / NAS 백업 정책
마지막 수정: 2026-01-18
```

### 잘 되는 쪽

- **Wiki.js** ✅ (메타데이터 깔끔)
- **Outline** ✅
- BookStack △
- DokuWiki ❌

------

## ③ 슬랙 → 위키 검색 (Slash Command / Bot)

> “슬랙에서 위키를 검색한다”

### 예시

```
/wiki VPN
```

→ 결과

```
1️⃣ VPN 접속 정책 (IT)
2️⃣ 외부 접속 가이드
3️⃣ 보안 장비 목록
```

### 이게 가능한 조건

- 문서 검색 API 제공
- 토큰 기반 인증
- 문서 권한 체크 가능

### 잘 되는 쪽

- **Wiki.js** ⭐⭐⭐⭐⭐
- Outline ⭐⭐⭐⭐
- BookStack ⭐⭐⭐
- XWiki ⭐⭐

👉 **AI 검색(RAG)**로 가려면
 이 단계가 사실상 **필수 전제조건**이야.

------

## ④ 슬랙 + AI (RAG / Copilot)

> “슬랙에서 질문하면 위키 기반으로 답해준다”

### 예

```
@company-ai VPN 접속 방법 알려줘
```

→ 답변

```
사내 VPN은 FortiClient 기반이며…
(출처: IT/VPN 정책 문서)
```

### 여기서 중요한 것

- 문서 Export / API
- Vector DB 연계
- 권한 기반 응답

### 가장 적합한 위키

- **Wiki.js** ✅ (API 구조 + DB 접근성)
- Outline ⚠️ (LDAP 약함)
- BookStack ⚠️ (추가 가공 필요)