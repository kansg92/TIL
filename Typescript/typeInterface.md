# TypeScript 선언 Type과 Interface

#### 공부목적

처음 `TypeScript`를 접했을 때는 `type`선언으로만 배웠음. 하지만 현업에서는 `Interface`형테로 작성하고 있어 이 둘의 차이를 은연중에만 알고 있어 차이를 명확히 알고  `TypeScript` 에대해 조금 더 심층적으로 공부함

---

## Interface VS Type

**코딩 스타일 일관성**을 위해 한 가지 방식만 사용하는 것을 권장

### Interface

- `TypeScript` 초창기 부터 존재한 구조로 **객체 지향 프로그래밍(OOP)**의 개념에 맞게 설계됨.
- 클래스의 `implements`와 연동되는 구조이기 때문에 OOP스타일 코드에 적합
- **확장성과 상호작용**에 중점을 둔 객체 타입 정의용
- **라이브러리/프레임워크와 연동하거나 클래스 기반 코드**와 함께 쓸 때
- 협업 코드에서는 **선언 병합이 유용할 수 있는 경우**
- 객체 지향 스타일, 클래스 구현, 병합 가능



### Type

- 이후에 추가된 기능으로 **타입 연산(유니언, 교차, 조건부 타입) 등**을 지원하기 위해 도입됨
- 좀 더 표현력이 풍부하고 유연한 타입 시스템을 제공하기 위한 목적
- **표현력과 조합성**에 중점을 둔 범용 타입 정의용
- **유니언 타입, 튜플, 복잡한 타입 조합**이 필요한 경우
- 더 유연하고 표현력 강함, 유니언/교차/튜플 가능



| 항목                          | `type`                                  | `interface`                       |
| ----------------------------- | --------------------------------------- | --------------------------------- |
| **용도**                      | 모든 타입 (객체, 유니언, 튜플 등)       | 주로 객체 타입                    |
| **확장(extends)**             | 다른 `type`을 확장할 수 있음 (`&` 사용) | `extends` 키워드로 다중 상속 가능 |
| **병합(Declaration Merging)** | ❌ 안 됨                                 | ✅ 가능                            |
| **유니언/교차 타입**          | ✅ 가능 (`A | B`, `A & B`)               | ❌ 불가능                          |
| **튜플/기본 타입 alias**      | ✅ 가능 (`type T = [number, string]`)    | ❌ 제한적                          |
| **구현 대상**                 | 타입 시스템 전용 (컴파일 타임)          | 클래스 구현 가능 (`implements`)   |
| **표현력**                    | 더 다양하고 복잡한 표현 가능            | 객체 중심, 직관적인 상속          |



### 사용 예시

#### 1. 객체 타입 정의

```typescript
interface User {
  name: string
  age: number
}

type UserType = {
  name: string
  age: number
}
```

둘 다 동일하게 동작.

#### 2.유니언/튜플/기본 타입 alias (interface 불가)

```typescript
type ID = string | number
type Pair = [string, number]
// interface로는 불가능
```

#### 3. 타입 확장 (둘 다 가능, 방식만 다름)

```typescript
interface A { a: number }
interface B extends A { b: number }

type C = { a: number }
type D = C & { b: number }

```

#### 4. 선언 병합 (interface만 가능)

```typescript
interface Person { name: string }
interface Person { age: number }

// 결과: { name: string; age: number }

type Person = { name: string }
type Person = { age: number } // ❌ 오류

```



### 타입선언 방식

- ## ✅ 1. **클래스를 이용한 타입 선언**

  TypeScript에서 `class`는 타입으로도 사용됨. 클래스가 정의되면 자동으로 해당 인스턴스의 타입도 함께 정의.

  ```typescript
  class User {
    name: string;
    constructor(name: string) {
      this.name = name;
    }
  }
  
  const u: User = new User("승기");
  ```

  - `User`는 **값(생성자)**이면서 **타입**으로도 사용됨
  - 클래스의 public 멤버들이 타입에 포함됨
  - `implements`로 `interface`를 적용할 수도 있음

  ------

  ## ✅ 2. **리터럴 타입 (Literal Types)**

  값 그 자체를 타입으로 사용할 수 있음

  ```typescript
  let direction: "left" | "right";
  direction = "left"; // OK
  direction = "up";   // ❌ 에러
  ```

  - `"left"`, `"right"` 자체가 타입
  - 종종 enum 대신 가볍게 사용됨

  ------

  ## ✅ 3. **타입 추론 (Type Inference)**

  TypeScript는 많은 경우 **자동으로 타입을 추론**.

  ```typescript
  const age = 30;
  // age: number로 추론됨
  
  const colors = ["red", "green", "blue"];
  // colors: string[]로 추론됨
  ```

  - 명시적 선언 없이도 타입이 생김
  - 복잡한 구조에서는 `as const`, `typeof`를 활용 가능

  ------

  ## ✅ 4. **`typeof`를 이용한 타입 추출**

  값으로 선언된 변수에서 타입을 추출

  ```typescript
  const config = {
    host: "localhost",
    port: 8080
  };
  
  type Config = typeof config;
  ```

  - `typeof`는 **런타임 값의 타입을 추출**하는 키워드
  - 주로 상수 객체에서 타입을 뽑을 때 유용

  ------

  ## ✅ 5. **`keyof`로 키 타입 생성**

  객체 타입의 키들을 타입으로 추출

  ```typescript
  type User = {
    id: number;
    name: string;
  };
  
  type UserKeys = keyof User; // "id" | "name"
  ```

  - 주로 **제네릭과 함께 동적 타입 처리**에 사용

  ------

  ## ✅ 6. **`as const` (리터럴 고정)**

  객체/배열 리터럴을 상수로 만들고, 타입을 더 좁게 고정

  ```typescript
  const roles = ["admin", "user", "guest"] as const;
  // 타입: readonly ["admin", "user", "guest"]
  
  type Role = typeof roles[number];
  // "admin" | "user" | "guest"
  ```

  - `as const`는 **리터럴을 변하지 않는 값**으로 만들어 타입을 좁힘
  - `typeof + [number]` 조합으로 유니언 타입 생성 가능

  ------

  ## ✅ 7. **제네릭(Generic) 타입**

  유연한 타입을 만들기 위해 사용됩니다.

  ```typescript
  type ApiResponse<T> = {
    data: T;
    error?: string;
  };
  
  const res: ApiResponse<number> = { data: 123 };
  ```

  - **타입 매개변수**를 받아 동적으로 구조를 생성할 수 있음
  - 라이브러리에서 매우 자주 사용됨

  ------

  ## ✅ 8. **유틸리티 타입 (내장 타입 조작 도구)**

  TypeScript는 여러 가지 내장 유틸리티 타입을 제공함.

  | 유틸리티 타입   | 설명                        |
  | --------------- | --------------------------- |
  | `Partial<T>`    | 모든 속성을 선택적으로 만듦 |
  | `Required<T>`   | 모든 속성을 필수로 만듦     |
  | `Pick<T, K>`    | 특정 키만 추출              |
  | `Omit<T, K>`    | 특정 키 제외                |
  | `Record<K, T>`  | 키-값 객체 생성             |
  | `ReturnType<T>` | 함수의 반환 타입 추출       |
  | `Parameters<T>` | 함수의 인자 타입 추출       |

  

  ```typescript
  ts복사편집type User = { id: number; name: string };
  type PartialUser = Partial<User>; // { id?: number; name?: string }
  ```

  ------

  ## ✅ 9. **조건부 타입 (Conditional Types)**

  타입의 조건 분기를 만들 수 있습니다.

  ```typescript
  type IsString<T> = T extends string ? "Yes" : "No";
  
  type A = IsString<string>; // "Yes"
  type B = IsString<number>; // "No"
  ```

  - 제네릭과 함께 쓰이며 복잡한 타입 연산 가능

  ------

  ## ✅ 10. **Mapped Types (매핑된 타입)**

  객체의 키에 따라 타입을 반복적으로 생성할 수 있음

  ```typescript
  type Flags<T> = {
    [K in keyof T]: boolean;
  };
  
  type User = { id: number; name: string };
  type UserFlags = Flags<User>; // { id: boolean; name: boolean }
  ```
