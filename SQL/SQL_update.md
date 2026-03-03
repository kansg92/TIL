# SQL_UPDATE





## select update



### 다른테이블 select해서 업데이트

```sql
UPDATE `TABLE_A` A
SET (A.`idx`, A.`column`, ...) = (
	SELECT B.`idx`, B.`COLUMN`, ...
    FROM `TABLE_B` B
    WHERE 1 = 1
	) 
WHERE condition
```



### JOIN 사용해서 업데이트

```sql
UPDATE TABLEA a
LEFT JOIN TABLEb zuci ON b.idx = a.user_idx
SET a.career_year = CEIL((zuci.coluimn + zuci.coluimn) / 12
```

