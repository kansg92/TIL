# Javascript map과 array비교



### 공부목적

코테중 indexof로 원하는 값을 찾았는데 몇개 문제중 시간 초과를 하게됨. 원인을 찾 던중 배열에서 indexof는 값이 클 수록 해당 값을 찾는데 큰 자원이 소모되는것을 알게되어 map을 이용하는것이 데이터양이 많아질 때 더 효율적인것을 알게되어서 해당 내용을 정리함.



- 테스트 문제
  - https://school.programmers.co.kr/learn/courses/30/lessons/178871
- 문제 설명

얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 `players`와 해설진이 부른 이름을 담은 문자열 배열 `callings`가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

------

##### 제한사항

- 5 ≤ players 의 길이 ≤ 50,000
  - `players[i]`는 i번째 선수의 이름을 의미합니다.
  - `players`의 원소들은 알파벳 소문자로만 이루어져 있습니다.
  - `players`에는 중복된 값이 들어가 있지 않습니다.
  - 3 ≤ `players[i]`의 길이 ≤ 10
- 2 ≤ callings의 길이 ≤ 1,000,000
  - `callings`는 `players`의 원소들로만 이루어져 있습니다.
  - 경주 진행중 1등인 선수의 이름은 불리지 않습니다.







- 처음 작성 답

```javascript
function solution(players, callings) {   
	callings.forEach(call => {
        const cur = players.indexof(call)
        if (cur <= 0) return
        const pre = cur - 1;
        [players[pre], players[cur]] = [players[cur], players[pre]];
    });
    
    return players;
}
```

- 수정한 답

```javascript
function solution(players, callings) {
    const indexMap = new Map(players.map((name, idx) => [name, idx]));
    callings.forEach(call => {
        const cur = indexMap.get(call);
        if (cur <= 0) return;

        const pre = cur - 1;
        const prevName = players[pre];
        const curName = players[cur];

        [players[pre], players[cur]] = [players[cur], players[pre]];

        indexMap.set(prevName, cur);
        indexMap.set(curName, pre);
    });
    
    return players;
}
```



처음 작성한 답은 indexof로 call index를 찾았고 2번째는 map을 먼저 만들어서 전체 players를 만들고 get과 set을 통해 스왑하여 데이터를 추적함.



## map과 indexof의 차이

### 시간복잡도

| 방식       | 시간 복잡도 | 설명                                     |
| ---------- | ----------- | ---------------------------------------- |
| `indexOf`  | O(n × m)    | `callings.length × players.length`       |
| `Map` 사용 | O(n + m)    | players → Map: O(n), callings 루프: O(m) |

indexOf의 경우 데이터가 많아질경우 곱으로 시간이 늘어남



### 왜 이런차이가 발생할까?

| 항목          | `indexOf()`                                 | `Map.get()`                                    |
| ------------- | ------------------------------------------- | ---------------------------------------------- |
| 대상 자료구조 | 배열 (`Array`)                              | 맵 (`Map`)                                     |
| 반환값        | 값이 **처음으로 나타나는 인덱스**           | 키에 **연결된 값**                             |
| 성능          | ❌ O(n) (배열을 앞에서부터 순회)             | ✅ O(1) (해시 기반 검색)                        |
| 사용 목적     | 배열 안의 **값**이 몇 번째에 있는지 찾을 때 | 키-값으로 구성된 데이터를 **빠르게 조회**할 때 |

| 항목              | `indexOf` (배열 기반)              | `get` (해시 기반 `Map`)                        |
| ----------------- | ---------------------------------- | ---------------------------------------------- |
| 자료구조          | **선형 리스트 (Array)**            | **해시 테이블 (Hash Table)**                   |
| 시간복잡도 (조회) | **O(n)**: 순차 탐색                | **O(1)** (평균), **O(n)** (최악)               |
| 검색 키           | **값(value)**                      | **키(key)**                                    |
| 내부 탐색 방식    | **앞에서부터 순회하며 `===` 비교** | **해시 함수를 통해 직접 주소 접근**            |
| 공간 효율         | 공간 사용 적음                     | 해시 충돌 처리 등으로 상대적으로 공간 소비     |
| 순서 보존         | 보존됨 (`Array`는 인덱스 기반)     | ES6 `Map`도 삽입 순서 보존됨 (단, 부수적 특성) |

코드 작성은 indexOf()를 사용한것이 더 짧고 간결하지만 컴퓨터가 자원을 먹는데 있어 indexOf()는 대용량 처리하기에는 위험한 함수라는 것을 알았음. 특히 대용량 데이터를 찾거나 할때는 map절대적으로 유리함.

### 내부 작동 구조 비교

#### 1. `indexOf()` -> 선형 탐색(Linear Search)

```javascript
const arr = ['a', 'b', 'c', 'd'];
arr.indexOf('c');

// 내부적으로는 이런식으로 동작함. 
for (let i = 0; i < arr.length; i++) {
  if (arr[i] === 'c') return i;
}
return -1;

```

- `===` 비교 연산으로 하나씩 순회

- Worst Case: 찾는 값이 마지막에 있거나 없음 → **전체 순회 (O(n**
- 전체 순회로 처음 코드에서 `forEach`를통해 n*m으로 반복문을 미친듯이 돌아가서 확인하게됨...

#### 2. `Map.get()` -> 해시 탐색 (Hash Table Lookup)

```javascript
const map = new Map([
  ['a', 0],
  ['b', 1],
  ['c', 2]
]);

map.get('c');

```

내부적으로는 이렇게 작동:

1. `'c'`에 대해 **해시 함수**를 적용 → 해시값(예: 3291)
2. 해시값을 인덱스로 **배열(버킷)에 접근**
3. 버킷에 충돌이 없다면 바로 값 반환 (**O(1)**)
4. 충돌이 있으면 **연결 리스트 또는 체이닝으로 탐색** (**O(k)**, 최악 O(n))



## 100만 건 조회 시

`players.length = 10,000` (데이터 1만 명)

`callings.length = 1,000,000` (호출 100만 건)

각 `call`에 대해 `players.indexOf(call)` 또는 `map.get(call)` 사용

- `indexOf`: **100만 번 × 평균 5000회 순회** = 수십억 연산 발생 가능
- `Map.get`: **100만 번 × 1회 조회** = 매우 빠름 (ms 단위)



### 둘중 언제 뭘 써야하나?

| 상황                                    | 적합한 자료구조                      |
| --------------------------------------- | ------------------------------------ |
| 순서 기반으로 값 처리, 데이터 적음      | `Array + indexOf`                    |
| 많은 항목에서 빠른 검색 필요            | `Map + get`                          |
| 값 자체가 고유 식별자처럼 쓰일 때       | `Map`                                |
| 키-값 관계 유지 + 빠른 접근이 필수일 때 | `Map` (혹은 `Object` for plain keys) |

CS관점으로 보았을 때 `indexOf`는 리스트에서 값 찾기에 적합하지만 성능은 선형 탐색 수준, `Map.get`은 해시 테이블의 핵심 연산, 정수 시간 접근이 가능. 단 모든 키가 같은 해시값 (`해시 충돌`) 인경우 문제가 생길 수 있어 체이닝 또는 오픈어드레싱을 통해 해결이 필요하며 더 많은 메모리를 사용한다.



