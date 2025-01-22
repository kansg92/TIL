# python basic





## List Comprehension

- 리스트를 쉽게, 짧게 한줄로 만들 수 있는 파이썬 문법

  - `[ ( 변수를 활용한 값 ) for ( 사용할 변수 이름 ) in ( 순회할 수 있는 값 )]`

  - ` arr = [i * 2 for i in range(size)]`

  - ` new_arr =[n * n for n in arr]`
  - `[A for row in arr]`

- 조건문 필터링
  - `[n for n in range(1, 11) if n % 2 == 0]`