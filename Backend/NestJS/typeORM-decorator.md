# TypeORM 데코레이터



### 기본구조

| 데코레이터                  | 설명                         | 예시                                                     |
| --------------------------- | ---------------------------- | -------------------------------------------------------- |
| `@Entity('table_name')`     | 테이블 이름 지정             | `@Entity('users') export class User {}`                  |
| `@PrimaryGeneratedColumn()` | 기본키 자동 증가 (INT 타입)  | `@PrimaryGeneratedColumn() id: number`                   |
| `@PrimaryColumn()`          | 기본키 직접 지정 (수동 관리) | `@PrimaryColumn() code: string`                          |
| `@Column()`                 | 일반 컬럼 정의               | `@Column({ type: 'varchar', length: 100 }) name: string` |
| `@Generated('uuid')`        | UUID 자동 생성 컬럼          | `@PrimaryGeneratedColumn('uuid') uuid: string`           |



### 날짜 / 시간 관리

| 데코레이터            | 설명                                | 예시                                    |
| --------------------- | ----------------------------------- | --------------------------------------- |
| `@CreateDateColumn()` | 레코드 생성 시 자동 날짜 입력       | `@CreateDateColumn() created_at: Date`  |
| `@UpdateDateColumn()` | 수정 시 자동 업데이트               | `@UpdateDateColumn() updated_at: Date`  |
| `@DeleteDateColumn()` | soft-delete용 컬럼 (실제 삭제 안함) | `@DeleteDateColumn() deleted_at?: Date` |



### 관계(Relation) 설정

| 데코레이터      | 설명                                        | 예시                                                |
| --------------- | ------------------------------------------- | --------------------------------------------------- |
| `@OneToOne()`   | 1:1 관계 설정                               | `@OneToOne(() => Profile, profile => profile.user)` |
| `@OneToMany()`  | 1:N 관계의 “1쪽” 정의                       | `@OneToMany(() => Post, post => post.user)`         |
| `@ManyToOne()`  | 1:N 관계의 “N쪽” 정의                       | `@ManyToOne(() => User, user => user.posts)`        |
| `@ManyToMany()` | N:N 관계 정의                               | `@ManyToMany(() => Role, role => role.users)`       |
| `@JoinColumn()` | 관계에서 외래키 지정 (1:1, N:1 등에서 사용) | `@JoinColumn({ name: 'user_id' })`                  |
| `@JoinTable()`  | N:N 중간 테이블 자동 생성                   | `@ManyToMany(() => Role) @JoinTable()`              |





### 컬럼 상세 옵션

| 옵션       | 설명                          | 예시                                                    |
| ---------- | ----------------------------- | ------------------------------------------------------- |
| `type`     | SQL 데이터 타입               | `@Column({ type: 'decimal', precision: 12, scale: 2 })` |
| `length`   | 문자열 길이 제한              | `@Column({ length: 50 })`                               |
| `nullable` | NULL 허용 여부                | `@Column({ nullable: true })`                           |
| `unique`   | 유니크 제약조건               | `@Column({ unique: true })`                             |
| `default`  | 기본값 지정                   | `@Column({ default: 0 })`                               |
| `comment`  | 컬럼 설명 (DDL 주석)          | `@Column({ comment: '계정 유형' })`                     |
| `select`   | 쿼리 시 기본 SELECT 제외 여부 | `@Column({ select: false }) password: string`           |



### 인덱스 및 제약조건

| 데코레이터                 | 설명                 | 예시                                |
| -------------------------- | -------------------- | ----------------------------------- |
| `@Index()`                 | 인덱스 지정          | `@Index() name: string`             |
| `@Index(['col1', 'col2'])` | 복합 인덱스          | `@Index(['user_id', 'created_at'])` |
| `@Unique(['email'])`       | 유니크 제약조건 지정 | `@Unique(['email'])`                |



###  Embedded / Transformer

| 데코레이터                 | 설명                           | 예시                                                     |
| -------------------------- | ------------------------------ | -------------------------------------------------------- |
| `@Embedded()`              | 다른 클래스를 하위 필드로 포함 | (TypeORM v0.3 이후는 `@Column(() => Class)`)             |
| `@Column({ transformer })` | 데이터 변환기 지정             | `{ to: val => encrypt(val), from: val => decrypt(val) }` |







## DTO



### class-validator 데코레이터

| 데코레이터            | 설명                       | 예시                                      |
| --------------------- | -------------------------- | ----------------------------------------- |
| `@IsString()`         | 문자열인지 확인            | `@IsString() name: string`                |
| `@IsInt()`            | 정수인지 확인              | `@IsInt() age: number`                    |
| `@IsNumber()`         | 숫자인지 확인 (float 포함) | `@IsNumber() price: number`               |
| `@IsBoolean()`        | 불리언 확인                | `@IsBoolean() active: boolean`            |
| `@IsDate()`           | 날짜 타입 확인             | `@IsDate() start_date: Date`              |
| `@IsEmail()`          | 이메일 형식 확인           | `@IsEmail() email: string`                |
| `@IsUUID()`           | UUID 형식 확인             | `@IsUUID() id: string`                    |
| `@IsEnum(EnumType)`   | enum 값 제한               | `@IsEnum(UserRole)`                       |
| `@IsArray()`          | 배열인지 확인              | `@IsArray() tags: string[]`               |
| `@IsOptional()`       | 선택적 필드                | `@IsOptional() memo?: string`             |
| `@Min(x)` / `@Max(x)` | 숫자 범위 제한             | `@Min(0) @Max(100)`                       |
| `@Length(min, max)`   | 문자열 길이 제한           | `@Length(3, 20)`                          |
| `@Matches(regex)`     | 정규식 검사                | `@Matches(/^[A-Za-z0-9]+$/)`              |
| `@ValidateNested()`   | 중첩 DTO 검증              | `@ValidateNested() @Type(() => ChildDto)` |

| 데코레이터                       | 설명                               | 예시                                         |
| -------------------------------- | ---------------------------------- | -------------------------------------------- |
| `@Type(() => Class)`             | 중첩 DTO 변환 시 타입 지정         | `@Type(() => AddressDto)`                    |
| `@Exclude()`                     | 직렬화 시 제외                     | `@Exclude() password: string`                |
| `@Expose()`                      | 직렬화 시 이름 지정 또는 선택 노출 | `@Expose({ name: 'userName' }) name: string` |
| `@Transform(({ value }) => ...)` | 값 변환                            | `@Transform(({ value }) => value.trim())`    |





