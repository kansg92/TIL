# 논리 / 조건 연산자 (Operator)



| 연산자 | 설명                                       | 비고                              |
| ------ | ------------------------------------------ | --------------------------------- |
| `      |                                            | `                                 |
| `??`   | Nullish - `null`/`undefined`일 때만 기본값 | 더 엄격한 조건                    |
| `&&`   | AND - falsy면 바로 반환                    | 조건 통과 시 실행에 자주 사용     |
| `?.`   | Optional Chaining                          | 안전하게 객체 접근(존재여부 체크) |
| `? :`  | 삼항 연산                                  | 간단한 조건문                     |
| `!`    | NOT                                        | Boolean 반전                      |



1. `??` (Nullish Coalescing Operator)
   - null 또는 undefined일 때만 오른쪽 값을 사용

```typescript
let b = undefined ?? 'default';  // 'default'
let c = 0 ?? 'default';  // 0
let d = '' ?? 'default';  // ''
let a = null ?? 'default';  // 'default'
```



2. `||` (Logical OR Operator)
   - **"Falsy" 값일 때** 오른쪽 값을 사용
   - "Falsy" 값: `false`, `0`, `''`, `null`, `undefined`, `NaN`

```typescript
console.log(0 || '기본값');         // 출력: '기본값'
console.log('' || '기본값');       // 출력: '기본값'
console.log(false || '기본값');    // 출력: '기본값'
console.log(null || '기본값');     // 출력: '기본값'
console.log(undefined || '기본값'); // 출력: '기본값'
```



`||` vs `|` 차이

```typescript
const a = false;
const b = true;

console.log(a || b); // true
console.log(a | b);  // 1   → false(0) | true(1) = 1

const x = 5; // 0b0101
const y = 3; // 0b0011

console.log(x || y); // 5  → x가 truthy이므로 x 반환
console.log(x | y);  // 7  → 0101 | 0011 = 0111 (7)

```





###  `$`비트연산자 `$`논리연산자 비교

```typescript
const a = true;
const b = false;

console.log('논리 AND (&&)');
console.log(a && b);  // false

console.log('비트 AND (&)');
console.log(a & b);   // 0  ← true는 1, false는 0 으로 변환되어 1 & 0 = 0

console.log('------');

const x = 5;  // 0b0101
const y = 3;  // 0b0011

console.log('비트 AND (&)');
console.log(x & y);  // 1  ← 0101 & 0011 = 0001

console.log('논리 AND (&&) 조건문 스타일');
console.log(x && y); // 3  ← x가 truthy니까 y 반환

```



2. `^` (비트 XOR)

   XOR (exclusive or): **다르면 1, 같으면 0**

| A    | B    | A ^ B |
| ---- | ---- | ----- |
| 0    | 0    | 0     |
| 0    | 1    | 1     |
| 1    | 0    | 1     |
| 1    | 1    | 0     |