# NestJS 프론트와 타입 공유



nestJS는 dto, entity등 타입을 강제하는 경우가 많은데 이러한 타입을 선언하고 만들고 프론트에서 만드는게 또 일인것 같아서 찾아보니 swagger를 통해서 프론트에 타입/SDK를 자동생성해서 할 수 있는 방법을 찾음

백엔드 DTO + Swagger 데코레이터로 스펙을 만들고 그걸로 프런트에 코드를 생성하는 방식.



## NestJS 관련 라이브러리 설치

```bash
npm add @nestjs/swagger swagger-ui-express # swagger 
npm i -D better-sqlite3 # DB접속을 우회하기위한 허구 DB모듈을 만들기위해 설치함

```



## 1 백엔드 Swagger 설정 + openAPI JSON 덤프

- swagger 설치

```bash
npm add @nestjs/swagger swagger-ui-express
```

- /src/mian.ts

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { DocumentBuilder, SwaggerModule } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  if (process.env.NODE_ENV !== 'production') {
    const config = new DocumentBuilder()
      .setTitle('Recap API')
      .setDescription('API docs')
      .setVersion('1.0.0')
      .build();
    const doc = SwaggerModule.createDocument(app, config);
    SwaggerModule.setup('docs', app, doc);
  }

  await app.listen(process.env.PORT ?? 3000);
}
bootstrap();

```

- dto.ts
  - dto파일에는 밑에와 같이 property를 선언해주어야함

```typescript
import { ApiProperty } from '@nestjs/swagger'
export class AccountDto {
  @ApiProperty() 
  idx : number;
  @ApiProperty() 
  ledger_idx : number;
  @ApiProperty() 
  user_idx : number;
  @ApiProperty() 
  name : string;
  @ApiProperty() 
  type : 'asset' | 'liability' | 'equity' | 'income' | 'expense';
  @ApiProperty({nullable: true}) 
  parent_idx! : number | null;
  @ApiProperty() 
  currency : string;
  @ApiProperty() 
  is_active : boolean;
  @ApiProperty() 
  sort_order : number;

  constructor(partial: Partial<AccountDto>) {
    Object.assign(this, partial);
  }
}
```



- src/scripts/dump-openapi.ts

```typescript
process.env.GEN_OPENAPI = '1'; // AppModule import 전에 세팅

import { NestFactory } from '@nestjs/core';
import { DocumentBuilder, SwaggerModule } from '@nestjs/swagger';
import { writeFileSync, mkdirSync } from 'node:fs';
import { join, dirname } from 'node:path';

async function run() {
  // 동적 import로 AppModule 읽기 (env 세팅 이후)
  const { AppModule } = await import('../src/app.module');
  const app = await NestFactory.create(AppModule, { logger: false });

  const config = new DocumentBuilder()
    .setTitle('Recap API')
    .setVersion('1.0.0')
    .addBearerAuth()
    .build();
  const doc = SwaggerModule.createDocument(app, config);

  const out = join(process.cwd(), '../contracts/openapi.json'); // 모노레포 기준
  mkdirSync(dirname(out), { recursive: true });
  writeFileSync(out, JSON.stringify(doc, null, 2));
  
  await app.close();
  process.exit(0);
}
run();

```

script파일을 생성해주는 ts작성.

- app.modules.ts

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { TypeOrmModule } from '@nestjs/typeorm';
import { RedisModule } from './redis/redis.module';

const IS_DOCGEN = process.env.GEN_OPENAPI === '1';

@Module({
  imports: [
    ConfigModule.forRoot({
      envFilePath: `.env_${process.env.NODE_ENV ?? 'debug'}`,
      isGlobal: true, // 전역 사용
    }),
    ...(!IS_DOCGEN ? [
      TypeOrmModule.forRootAsync({
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
      })
    , RedisModule] :[
      TypeOrmModule.forRoot({
        type: 'better-sqlite3',     
        database: ':memory:',
        autoLoadEntities: true,      // forFeature 유지 가능
        synchronize: false,
        logging: false,
      }),
    ]),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}

```

그냥 실행시 DB연결때문에 오류가 있는것 같아서 문서 만들때는 better-sqlite3로 허상DB연결을해서 우회를 하는 방향을 선택함.
특히 forFeature는 각 모듈마다 쓰는 경우가 있는데 이걸 전체 우회하기위해 허상DB연결이 편할것 같았음.

- package.json

```typescript
{
  "scripts": {
    "build:openapi": "ts-node -T scripts/dump-openapi.ts"
  }
}

```

scripyts 문을 추가하여 사용



## 프론트엔드



### orval에 axios주입용 뮤테이터 추가

- src/api/axios-mutator.ts

```typescript
import type { AxiosRequestConfig, AxiosResponse } from 'axios'
import $axios from './axios'

// orval이 모든 요청을 여기로 태워 보냅니다.
export const axiosInstance = <T = unknown, R = AxiosResponse<T>>(config: AxiosRequestConfig): Promise<R> => {
  return $axios.request<T, R>(config)
}

```

 

### orval 설정

- oravfal.config.cjs

```typescript
/** @type {import('orval').Config} */
module.exports = {
  recap: {
    input: '../contracts/openapi.json',   // 백엔드가 덤프한 파일
    output: {
      target: 'src/api/sdk',              // 생성될 SDK 경로
      client: 'axios',
      mode: 'split',                      // 태그별 파일 분리 (ex. accounts, auth 등)
      prettier: true,
      override: {
        mutator: {
          path: 'src/api/axios-mutator.ts',
          name: 'axiosInstance',
        },
        // 선택: 응답 unwrap(axios의 {data}만 꺼내서 반환하고 싶으면)
        // transformer: './src/api/unwrap-transformer.cjs',
      },
    },
  },
}

```

### 프론트 scripts

```json
{
  "scripts": {
    "gen:openapi": "cd ../backend && pnpm build:openapi",
    "gen:sdk": "orval --config orval.config.cjs",
    "gen": "pnpm gen:openapi && pnpm gen:sdk"
  }
}

```



