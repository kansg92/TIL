# Outline



outline 서버 세팅



docker 설치

Nginx+SSL 적용



.env 설정...



ldap연동..

- authentik
  - outline 연동 가이드 공식 문서 존재
  - OIDC/SAML 등 표준 지원 + (LDAP를 뒤에 물리기 쉬움)
  - UI/Flow가 좋아서 “위키 사용자/그룹 운영”까지 생각하면 관리가 편함

일단 outline서버에서 보험으로 돌릴거라 swap파일 만들기( AI추천...)

```
#스왑 파일 만들기
sudo fallocate -l 4G /swapfile 
#권한 잠그기 (보안 필수)
sudo chmod 600 /swapfile
#스왑으로 포맷
sudo mkswap /swapfile
#스왑 활성화
sudo swapon /swapfile
#재부팅 후에도 유지
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
#확인
swapon --show
free -m
```

```
OIDC_CLIENT_ID=xxxxxxxx
OIDC_CLIENT_SECRET=yyyyyyyy
OIDC_AUTH_URI=https://auth.zeroton.co/application/o/authorize/
OIDC_TOKEN_URI=https://auth.zeroton.co/application/o/token/
OIDC_USERINFO_URI=https://auth.zeroton.co/application/o/userinfo/
OIDC_LOGOUT_URI=https://auth.zeroton.co/application/o/default-provider-invalidation-flow/end-session/
OIDC_USERNAME_CLAIM=preferred_username
OIDC_DISPLAY_NAME=ZIP
OIDC_SCOPES=openid profile
```



우리 ldap서버에는 email이없는데 outline에서는 email이 필수여서 무조건 들어야갸함,

`속성 -> 사용자매핑`  

```
uid = user.username
if not uid:
    return {}

return {
    "email": f"{uid}@zeroton.co",
    "email_verified": True,
}

```

통해 임시(가짜)메일을 생성하여 매칭시켜 로그인할수 있도록함.





- dex
  - Dex는 커넥터(예: LDAP)로 붙고 OIDC를 내주는 “경량 브릿지” 성격이 강함
  - 대신 **관리 UI/권한정책/MFA 같은 IAM 기능은 기대하면 아쉬움**(대개 쿠버네티스/내부 인증 브릿지 용도로 많이 씀)
- **keycloak** --> 너무 무거워서 탈락...
  - 전통적인 엔터프라이즈 IAM 강자. OIDC/SAML, 브로커링, LDAP/AD 연동 등 폭이 넓음 
  - 다만 **구성과 개념이 무겁고** 운영 난이도가 authentik보다 올라가는 편(초기 러닝/설정 비용)



### slack 연동

## 1) Slack 앱(봇) 만들기

### A. 앱 생성

1. Slack API 페이지 → **Create New App**
2. **From scratch**
3. 워크스페이스 선택
4. App Name: `wiki-bot` 같은 이름

### B. Bot 기능 켜기

- **Features → App Home**
  - “App Display Name / Bot Name” 확인
- **Features → OAuth & Permissions**
  - 아래 **Bot Token Scopes** 추가:
    - `chat:write` (답장)
    - `app_mentions:read` (채널 멘션 읽기)
    - `im:history` (DM 읽기)

그리고 **Install to Workspace** 눌러서 설치
 → 여기서 **Bot User OAuth Token (xoxb-...)**가 생김 = `SLACK_BOT_TOKEN`

### C. Socket Mode 켜기 (핵심)

- **Settings → Socket Mode**
  - Enable Socket Mode: ON
  - **Generate an App-Level Token**
    - Token Name: `wiki-bot-socket`
    - Scopes: `connections:write`
  - 생성되면 **xapp-...** 토큰이 나옴 = `SLACK_APP_TOKEN`

### D. 이벤트 구독(멘션 + DM)

- **Features → Event Subscriptions**
  - Enable Events: ON
  - Subscribe to bot events:
    - `app_mention`
    - `message.im`

### E. 서명 시크릿 복사

- **Settings → Basic Information**
  - **Signing Secret** 복사 = `SLACK_SIGNING_SECRET`

✅ 지금 네 손에 있어야 하는 3개

- `SLACK_BOT_TOKEN` = `xoxb-...`
- `SLACK_APP_TOKEN` = `xapp-...` (Socket Mode용)
- `SLACK_SIGNING_SECRET` = `...`

------

## 2) 봇 서버(가장 간단한 Node + Bolt)

### A. 폴더 준비

```
mkdir wiki-bot && cd wiki-bot
npm init -y
npm i @slack/bolt
```

### B. `index.js` (DM/멘션 둘 다 처리)

```
import { App } from "@slack/bolt";

const app = new App({
  token: process.env.SLACK_BOT_TOKEN,
  signingSecret: process.env.SLACK_SIGNING_SECRET,
  socketMode: true,
  appToken: process.env.SLACK_APP_TOKEN,
});

// 채널에서 @멘션하면 스레드로 답
app.event("app_mention", async ({ event, say }) => {
  // 봇 메시지 무한루프 방지
  if (event.bot_id) return;

  await say({
    thread_ts: event.ts,
    text: "✅ wiki-bot 연결 완료! (채널 멘션 테스트 성공)",
  });
});

// DM으로 오면 DM으로 답
app.message(async ({ message, say }) => {
  // DM만 처리 (message.channel_type === 'im')
  if (message.channel_type !== "im") return;
  if (message.bot_id || message.subtype === "bot_message") return;

  await say("✅ wiki-bot 연결 완료! (DM 테스트 성공)");
});

await app.start();
console.log("⚡️ wiki-bot is running (Socket Mode)");
```

### C. 실행

```
export SLACK_BOT_TOKEN="xoxb-..."
export SLACK_APP_TOKEN="xapp-..."
export SLACK_SIGNING_SECRET="..."
node index.js
```

------

## 3) 테스트

1. Slack에서 봇이 있는 채널에서:

- `@wiki-bot 안녕`
   → 스레드로 “채널 멘션 테스트 성공”이 오면 OK

1. 봇 프로필 들어가서 DM 열고:

- “안녕”
   → “DM 테스트 성공” 오면 OK

------

## 4) (옵션) docker-compose로 띄우기

원하면 봇도 compose에 넣을 수 있어. 예:

```
services:
  wiki-bot:
    build: ./wiki-bot
    environment:
      SLACK_BOT_TOKEN: "xoxb-..."
      SLACK_APP_TOKEN: "xapp-..."
      SLACK_SIGNING_SECRET: "..."
    restart: unless-stopped
```



## Rag를 위한 vectorDB 구축 (pgvector)

pgvector로 가면:

- 문서 chunk를 벡터로 저장 → **한글 자연어도 유사 의미로 검색 가능**
- Outline search가 0건이어도 상관 없음 (retrieval이 독립됨)
- docId/title/url 같은 메타를 테이블로 붙이기 쉬움 → 답변에 링크 정확히 포함
- 업데이트/동기화 배치도 안정적으로 만들기 좋음

### pgvector 운영형 MVP에서 해야 할 일 덩어리

1. **RAG 전용 Postgres 준비**

- 새 DB(또는 새 스키마) + pgvector extension
- 네트워크/계정/권한
- (선택) 백업 정책/볼륨

1. **스키마 설계**

- `documents`(docId, title, url, updatedAt, collectionId…)
- `chunks`(chunkId, docId, chunkIndex, text, embedding vector, hash…)
- 인덱스(메타 + 벡터)

1. **동기화 파이프라인**

- Outline API로 문서 목록/수정시간 확인
- 변경된 문서만 가져오기(증분)
- chunking → embedding 생성 → upsert
- 삭제/아카이브 처리(soft delete 권장)

1. **검색 + 답변**

- 질문 embedding → top-k chunk 검색
- (권장) 필터: collectionId / published / archived
- Gemini에 컨텍스트 주입 + 링크 반환

1. **운영 요소**

- 크론/스케줄러(동기화 주기)
- 로깅/모니터링(최소)
- 백업(볼륨 스냅샷 or pg_dump)



- 기존 EC2에 **Postgres+pgvector 컨테이너** 하나 추가
- 봇/동기화는 Outline API로 문서를 읽어서
- **RAG DB(=pgvector)**에 chunk+embedding 저장
- 질문 들어오면 **벡터 검색 top-k** → Gemini 답변

> Gemini Embedding은 `ai.models.embedContent({ model:'gemini-embedding-001' ... })`로 가능 
>  pgvector 도커 이미지는 `pgvector/pgvector:pg16` 같은 공식 이미지가 있음 

------

# 1) 폴더 구조 (추천)

EC2에서 작업 폴더 하나 만들고:

```
rag-wiki-bot/
  docker-compose.yml
  .env
  db/
    01_init.sql
  bot/
    package.json
    index.js
```

------

# 2) docker-compose.yml (pgvector DB + 봇)

```
services:
  ragdb:
    image: pgvector/pgvector:pg16
    container_name: ragdb
    environment:
      POSTGRES_USER: rag
      POSTGRES_PASSWORD: ragpassword
      POSTGRES_DB: ragdb
      TZ: Asia/Seoul
    ports:
      - "5433:5432"     # 기존 5432 쓰고 있으면 5433 권장
    volumes:
      - ragdb_data:/var/lib/postgresql/data
      - ./db/01_init.sql:/docker-entrypoint-initdb.d/01_init.sql:ro
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U rag -d ragdb"]
      interval: 5s
      timeout: 3s
      retries: 20
    restart: unless-stopped

  wiki-bot:
    build:
      context: ./bot
    container_name: wiki-bot
    env_file:
      - ./.env
    depends_on:
      ragdb:
        condition: service_healthy
    restart: unless-stopped

volumes:
  ragdb_data:
```

> 포인트: DB 데이터는 `ragdb_data` 볼륨으로 영속화(운영형 기본)

------

# 3) db/01_init.sql (스키마 + 인덱스)

이게 “운영형 MVP”의 핵심이야.

- 문서 메타(`wiki_documents`)
- 청크 + 임베딩(`wiki_chunks`)
- **FTS(GIN)** + **벡터(HNSW)** 둘 다 준비 (하이브리드로 갈 수 있게)

```
CREATE EXTENSION IF NOT EXISTS vector;

-- (선택) 한글/유사어/부분일치에 유용한 trigram을 쓰고 싶으면
-- CREATE EXTENSION IF NOT EXISTS pg_trgm;

CREATE TABLE IF NOT EXISTS wiki_documents (
  doc_id        text PRIMARY KEY,          -- Outline document.id
  title         text NOT NULL,
  url           text NOT NULL,
  collection_id text,
  updated_at    timestamptz,
  fetched_at    timestamptz NOT NULL DEFAULT now(),
  content_hash  text                         -- 본문 변경 감지용(sha256 같은)
);

CREATE TABLE IF NOT EXISTS wiki_chunks (
  chunk_id      bigserial PRIMARY KEY,
  doc_id        text NOT NULL REFERENCES wiki_documents(doc_id) ON DELETE CASCADE,
  chunk_index   int NOT NULL,
  content       text NOT NULL,
  -- pgvector: dimension 고정이 일반적이지만, 임베딩 차원 바뀔 여지 대비해서 "vector"로 두고
  -- 인덱스는 model_id+캐스팅(부분 인덱스)로 운영 가능 (필요시 단순화 가능)
  embedding     vector,
  model_id      text NOT NULL DEFAULT 'gemini-embedding-001',
  content_hash  text NOT NULL,               -- chunk 단위 변경 감지
  created_at    timestamptz NOT NULL DEFAULT now(),
  updated_at    timestamptz NOT NULL DEFAULT now(),
  UNIQUE (doc_id, chunk_index)
);

-- FTS(키워드) 인덱스: 나중에 hybrid 검색에 도움
ALTER TABLE wiki_chunks
  ADD COLUMN IF NOT EXISTS tsv tsvector
  GENERATED ALWAYS AS (to_tsvector('simple', coalesce(content,''))) STORED;

CREATE INDEX IF NOT EXISTS idx_wiki_chunks_doc_id ON wiki_chunks(doc_id);
CREATE INDEX IF NOT EXISTS idx_wiki_documents_updated_at ON wiki_documents(updated_at);
CREATE INDEX IF NOT EXISTS idx_wiki_chunks_tsv ON wiki_chunks USING GIN(tsv);

-- 벡터 인덱스 (HNSW)
-- cosine distance 인덱스 예시. (pgvector는 cosine용 ops 제공) :contentReference[oaicite:2]{index=2}
-- ⚠️ embedding 차원을 768로 고정해서 쓸 계획이면 아래 cast 부분을 vector(768)로 맞추고,
--     앱에서 embedContent 요청도 outputDimensionality=768로 맞추는 걸 추천.
--     (MVP에선 일단 index 없이 시작 -> 데이터 쌓인 뒤 index 생성도 가능)
CREATE INDEX IF NOT EXISTS idx_wiki_chunks_hnsw_cosine
  ON wiki_chunks
  USING hnsw ((embedding::vector(768)) vector_cosine_ops)
  WHERE model_id = 'gemini-embedding-001';
```

참고로 pgvector는 vector 차원을 고정해서 쓰는 게 일반적이고, HNSW 인덱스 생성/옵션도 공식적으로 지원돼 
 또한 `vector`(무차원) 타입도 가능하지만, **인덱스는 동일 차원끼리**가 전제라 위처럼 부분 인덱스/캐스팅을 쓰는 방식이 문서에 나와 있어 

------

# 4) .env 예시 (봇 + Outline + RAG DB)

`.env`는 루트에:

```
# Slack
SLACK_BOT_TOKEN=xoxb-...
SLACK_SIGNING_SECRET=...
SLACK_APP_TOKEN=xapp-...

# Outline
OUTLINE_BASE_URL=https://wiki.zeroton.co
OUTLINE_API_KEY=ol_...

# Gemini
GOOGLE_API_KEY=...

# RAG DB (docker-compose에서 5433으로 열었으니)
RAG_DATABASE_URL=postgres://rag:ragpassword@ragdb:5432/ragdb
# (컨테이너 밖에서 접속할 땐 localhost:5433)
```

------

# 5) bot/package.json (최소 의존성)

```
bot/package.json
{
  "name": "wiki-rag-bot",
  "type": "module",
  "dependencies": {
    "@slack/bolt": "^3.20.0",
    "@google/genai": "^0.6.0",
    "pg": "^8.12.0"
  }
}
```

그리고 `bot/Dockerfile` (compose에서 build 하려면 필요) --> Dockerfile 생성

```
FROM node:20-alpine
WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm install --omit=dev
COPY . .
CMD ["node", "index.js"]
```





ragdb확인

`docker exec -it ragdb psql -U rag -d ragdb`











## 백업자동화하기..







## outline 내부사용자... 



