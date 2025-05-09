# Vue 에서 ref 와 reactive



`ref`와 `reactive`는 vue3에서 Composition API에서 반응형 상태를 만들기 위한 두가지 방식이다.



### 차이점 요약

| 항목         | `ref`                                                 | `reactive`                       |
| ------------ | ----------------------------------------------------- | -------------------------------- |
| 대상         | **기본형 (primitive)** 값                             | **객체 (object, array)** 전체    |
| 사용 시 접근 | `.value` 필요 (`ref.value`)                           | 바로 사용 가능 (`reactive.prop`) |
| 내부 구현    | 내부적으로 `reactive({ value: x })`                   | Proxy를 이용해 객체를 감싼다     |
| Unwrap       | 템플릿에서는 자동 언랩됨 (`ref.value` 없이 사용 가능) | 자동 언랩 불가                   |





| 상황                          | 유리한 방식                      | 이유                                       |
| ----------------------------- | -------------------------------- | ------------------------------------------ |
| 단일 숫자/문자/불린           | `ref`                            | 간단하고 명확                              |
| 객체 전체를 반응형으로 관리   | `reactive`                       | 구조를 유지한 채 반응형 처리 가능          |
| `watch`나 `computed`에서 추적 | `ref` 또는 `reactive` 둘 다 가능 | 단, 객체는 `reactive.obj.prop` 단위로 추적 |
| 배열에 값을 푸시하거나 변경   | `reactive` 또는 `ref([])`        | 변경 방식에 따라 선택                      |



object인경우 `ref`는 재할당 해도 반응형을 유지하지만 `reactive`는 재할당시 반응형을 잃어버림

`ref`는 사용시 `.value` `reactive`는 그냥 사용 가능.



reactive는 언제 사용할까?

현재 reactive는 동적으로 키추가를 사용하여 pending값으로 사용중임

`const reg_pending = reactive<Record<string, boolean>>({})`

이런식으로 키값이 정해지도 각 배열의 키값을 키로 값을 boolean으로 사용

다양한 상태를 구조화 하여 관리가 가능한 경우 reactive를 사용



