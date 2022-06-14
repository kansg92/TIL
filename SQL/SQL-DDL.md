# SQL DDL문

DDL의 명령어로는 create, alter, drop, truncate, rename이 있다.



### CREATE

```SQL
CREATAE TABLE 테이블명{
	컬럼명 데이터타입(사이즈);
	id VARCHAR(30) NOT NULL;
	name VARCHAR(20);
	price INT NOT NULL;
	regdate DATE;
}
```



### ALTER

- 테이블의 특정 컬럼을 삭제하거나 추가 또는 변경할 때 사용하는 명령어.

```SQL
-- 컬럼 추가
ALTER TABLE 테이블명 ADD 새로운컬럼명 데이터타입(사이즈);

-- 컬럼 수정
ALTER TABLE 테이블이름 MODIFY 기존컬럼명 데이터타입(사이즈)<변경>;

-- 컬럼 삭제
ALTER TABLE 테이블명 DROP COLUMN 컬럼명;

-- 테이블 읽기전용으로 변경
ALTER TABLE 테이블명 READ ONLY;
```



### DROP, RENAME

```SQL
-- TABLE 삭제
DROP TABLE 테이블명;

-- TABLE 이름 변경
RENAME 기존테이블명 TO 변경테이블명
```

