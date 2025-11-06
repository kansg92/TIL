# nestJS



##  사용이유

- 사이드 프로젝트 백앤드를 그냥 nodeJS로 구성해보고 싶었음.
- 가장 많이 사용하는 express 와 nestJS를 비교하고 고민 했었음
- nestJS가 express에 비해 typescript와 더 친화적이며 타입안정성이 좋을 것 같아서 nestJS를 선택해서 사용함.



### 백앤드 nodeJS 비교

#### Express.js 

- **가장 널리 쓰이는 경량 웹 프레임워크**
- 빠르게 REST API, 서버 구축 가능
- 미들웨어 중심 구조

✅ **장점**

- 러닝커브 낮음 (빠른 시작 가능)
- 대규모 생태계 & 자료 풍부
- 다른 라이브러리와 유연하게 조합 가능

❌ **단점**

- 구조화가 부족해서 규모가 커지면 코드 복잡도 ↑
- 타입스크립트 지원은 있지만 기본적

🔧 **추천 상황**

> 소규모 프로젝트, 빠른 프로토타이핑, REST API 서버

#### nestJS

- Express(또는 Fastify) 위에서 동작하는 **TypeScript 기반의 풀스택 프레임워크**
- Angular 스타일의 모듈/의존성 주입 구조

✅ **장점**

- 타입스크립트 기반으로 대규모 프로젝트에 적합
- 모듈화 / DI / 데코레이터 기반 아키텍처
- 테스트, 문서화 등 엔터프라이즈 기능 내장

❌ **단점**

- 러닝 커브가 다소 있음
- 간단한 프로젝트엔 오버킬일 수도

🔧 **추천 상황**

> 중대형 서비스, 팀 프로젝트, 유지보수 고려한 구조적 개발

#### Fastify

- Express보다 더 빠르고 현대적인 Node.js 웹 프레임워크

✅ **장점**

- 성능 좋고 경량
- JSON Schema 기반의 요청/응답 검증
- 공식 NestJS와도 연동 가능

❌ **단점**

- 익숙하지 않은 스타일일 수 있음
- 생태계는 Express보단 작음

🔧 **추천 상황**

> 고성능이 필요한 REST API 서버

## nestJS 초기 구현 및 셋팅



1. NestJS CLI 설치

`npm i -g @nestjs/cli`

2. 프로젝트 생성

`nest new my-backend-api`

3. 기본 폴더 구조 (MVC패턴을 따르는듯...?)

```````yaml
src/
├── app.module.ts       ← 앱 루트 모듈
├── main.ts             ← 엔트리 포인트
├── users/              ← 예시: 사용자 도메인
│   ├── users.controller.ts   ← C: Controller (Route handler)
│   ├── users.service.ts      ← V: Service (비즈니스 로직)
│   ├── users.module.ts       ← 모듈 (의존성 관리)
│   └── entities/
│       └── user.entity.ts    ← M: Model (DB Entity)
```````

4. 서버 실행(dev는 빼도됨)

`npm run start:dev`

빌드 : `npm run build`

프로덕트 실행 : `npm run start:prod`

기본 스크림트들...

```````json
  "scripts": {
    "build": "nest build",
    "format": "prettier --write \"src/**/*.ts\" \"test/**/*.ts\"",
    "start": "nest start",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "start:prod": "node dist/main",
    "lint": "eslint \"{src,apps,libs,test}/**/*.ts\" --fix",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json"
  },
  
```````



프론트앤드(vue)와 연결시 304를 게속해서 vue에서 뺏어가는 문제가 있었음... vue에서 2시간동안 뻘짓을 해봤는데 build를 해보고 다시 실행하니 서버와 연결이 되었음... axios문제인지.. vue proxy문제인지 정확히 모르겠지만 build를 해보는 습관을 갖는게 좋을 것 같음



## NestJS DB connection

1. 패키지설치

`npm install --save @nestjs/typeorm typeorm mysql2`

`mysql12`는 MYSQL 드라이버 역할

2. .env 파일 설정

   ```
   MYSQL_DATABASE_HOST = ''
   MYSQL_DATABASE_DB = ''
   MYSQL_DATABASE_USER = ''
   MYSQL_DATABASE_PASSWORD = ''
   MYSQL_DATABASE_CHARSET = ''
   ```

3. `app.module.ts` 

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    UsersModule,
    ConfigModule.forRoot({ 
      envFilePath: `.env_${process.env.NODE_ENV ?? 'debug'}`, // NODE_ENV에 따라 env파일 사용
      isGlobal: true, // 전역 사용
    }),
    TypeOrmModule.forRootAsync({ // DB connection
      inject: [ConfigService],
      useFactory: (config: ConfigService) => ({
        type: 'mysql',
        host: config.get('MYSQL_DATABASE_HOST'),
        username: config.get('MYSQL_DATABASE_USER'),
        password: config.get('MYSQL_DATABASE_PASSWORD'),
        database: config.get('MYSQL_DATABASE_DB'),
        charset: config.get('MYSQL_DATABASE_CHARSET'),
        synchronize: false,
        autoLoadEntities: true,
        logging: true,
      }),
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```



4. `service.ts`

```typescript
import { Injectable } from '@nestjs/common';
import { UserDto } from './createUser.dto';
import { DataSource } from 'typeorm';

@Injectable()
export class UsersService {
  // dbconn..
  constructor(private readonly dataSource: DataSource) {}   

  // 비동기 promise타입으로 함수를 만들어야함...
  async findAllQuery(): Promise<UserDto[]> {
    const items = await this.dataSource.query<UserDto[]>(
      'SELECT * FROM users',
    );
    return items;
  }
    
}

```



### async/await 패턴을 쓰는 이유

1. 가장 직관적이고 깔끔한 코드임.
2. async는 promise를 반환하고 await는 응담이 될때까지 기다려줌(비동기)
3. await를 안쓰게 된다면 promise<pending> 으로 응담결과가 나와서 비동기를 써야함
4. Nest의 예외 처리 / 응답 처리와 자연스럽게 동작함
5. 유지보수/협업에 강함

