# SQL_UPDATE





## select update



### 다른테이블 select해서 업데이트

```sql

```



### JOIN 사용해서 업데이트

```sql
UPDATE TABLEA a
LEFT JOIN TABLEb zuci ON b.idx = a.user_idx
SET a.career_year = CEIL((zuci.coluimn + zuci.coluimn) / 12
```

