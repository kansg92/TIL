# SQL 서브쿼리 

## 1) CTE (Common Table Expression, `WITH ... AS (...)`)

**무엇?**
 쿼리의 맨 앞에서 임시 결과집합에 “이름”을 붙여서 아래 본문에서 재사용하는 문법.

**어떻게 실행?**

- MySQL 8.0은 기본적으로 **CTE를 인라인(풀어쓰기)** 하여 최적화하는 경향이 큽니다. (일부 경우 **물질화(materialize)** 가능)
- MariaDB도 유사하지만, 버전/옵티마이저 옵션에 따라 materialize 여부가 달라질 수 있습니다.
- **재귀 CTE**(WITH RECURSIVE)는 CTE만의 고유 기능.

**장점**

- 가독성 최고: 복잡한 서브쿼리를 위로 빼서 **이름**으로 부를 수 있어요.
- 여러 번 **재사용** 가능(동일 정의를 반복 타이핑 X).
- **재귀**가 필요하면 CTE가 답.

**단점**

- 예전 버전/특정 상황에서 **물질화**로 인해 오히려 느려질 수 있음(임시 테이블 생성, 메모리/디스크 I/O).
- 동일 로직이 한 번만 쓰이고, 최적화가 잘 되는 경우엔 파생 테이블과 성능상 큰 차이 없음.

**언제?**

- 읽기/유지보수성 중시.
- 같은 중간결과를 **여러 번** 써야 할 때.
- **재귀 쿼리**가 필요할 때(예: 계층 구조).



```sql
WITH ht_one AS (
  SELECT etan, MAX(written_date) AS written_date
  FROM hometax_teet
  GROUP BY etan
)
SELECT ...
FROM doc_expenditures E
LEFT JOIN ht_one H ON H.etan = E.etan
WHERE E.doc_idx = 0;
```

## 2) 파생 테이블 (Derived Table, FROM 절의 서브쿼리)

**무엇?**
 `FROM (SELECT ...) AS 별칭` 형태로 **한 번 계산한 중간결과**를 바깥 쿼리에서 테이블처럼 조인하는 방식.

**어떻게 실행?**

- 옵티마이저가 파생 테이블을 **인라인** 하거나 **물질화**할 수 있음(버전/옵션/쿼리 형태에 따라).
- 인덱스는 파생 테이블 자체에 생성할 수 없지만(임시), **원본 테이블의 인덱스**와 GROUP BY/ORDER BY 최적화가 중요.

**장점**

- **한 번 그룹→조인** 패턴에 강함. (예: etan별 MAX 한 번 뽑고 E와 조인)
- 바깥에서 **명확한 조인 계획**을 갖게 되어 실행 계획이 직관적일 때가 많음.
- CTE보다 **짧고 직관적**일 수 있음.

**단점**

- 파생 테이블이 **큰 집합**이면 임시 테이블 I/O가 커질 수 있음.
- 중간결과를 **여러 번 재사용**해야 하면 CTE만큼 우아하지 않음(반복 타이핑).

**언제?**

- 메인 쿼리에서 조인하기 전에 **집계/정제**를 한 번 하고 싶을 때.
- 결과 세트가 크지 않거나, **원본 인덱스** 덕에 집계가 저렴할 때.

**예시**

```sql
SELECT ...
FROM doc_expenditures E
LEFT JOIN (
  SELECT etan, MAX(written_date) AS written_date
  FROM hometax_teet
  GROUP BY etan
) H ON H.etan = E.etan
WHERE E.doc_idx = 0;
```

## 3) 상관 서브쿼리 (Correlated Subquery)

**무엇?**
 바깥 쿼리의 각 행(E.etan)을 받아 **행마다 실행**되는 서브쿼리.

**어떻게 실행?**

- 바깥 행 수 N에 대해, 서브쿼리를 **N번** 평가.
- 하지만 **적절한 인덱스**가 있으면 각 평가가 “인덱스 점프 + LIMIT 1” 수준이라 매우 저렴할 수 있음.

**장점**

- **가장 직관적/간단**: “각 etan에 대해 최신 1건만 주세요”를 그대로 표현.
- `(etan, written_date)` 인덱스가 있으면 **매우 빠름**: 인덱스 범위 스캔 후 **ORDER BY DESC LIMIT 1**.

**단점**

- 바깥 결과 N이 **매우 큰 경우**, N번 반복의 총비용이 커질 수 있음.
- 인덱스 없으면 테이블 스캔이 반복되어 느려짐.

**언제?**

- 바깥 결과가 **적당히 작거나** (수백~수천), 인덱스가 잘 잡혀 **행당 조회가 O(log M)** 수준일 때.
- 코드 **간결성**을 우선할 때.

**예시**

```sql
SELECT
  E.*,
  (
    SELECT HT.written_date
    FROM hometax_teet HT
    WHERE HT.etan = E.etan
    ORDER BY HT.written_date DESC
    LIMIT 1
  ) AS teet_written_date
FROM doc_expenditures E
WHERE E.doc_idx = 0;
```

------

## 성능의 핵심: “인덱스 + 카디널리티 + N과 M의 크기”

- **필수 인덱스 권장**
  - `hometax_teet (etan, written_date)`  ← 최신 1건 찾기의 핵심
  - `doc_expenditures (doc_idx)` + (필요 시) `(doc_idx, etan)` 또는 `etan` 단일 보조
- **N(= E의 결과 행 수), M(= teet의 전체 행 수)** 에 따라 선택:
  - **N이 작다** → **상관 서브쿼리**가 보통 가장 간단하고 빠름.
  - **N이 크다** → **파생 테이블/CTE**로 **한 번 그룹** 후 조인하는 편이 총비용이 안정적.
- **CTE vs 파생 테이블**: 성능은 대체로 비슷합니다(최적화기 재작성/물질화 여부에 좌우). **가독성/재사용성**을 기준으로 고르세요. (재귀 필요하면 무조건 CTE)