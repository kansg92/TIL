# day18__MySQL2

### SELECT2

```SQL
SELECT * FROM buytbl;

SELECT * FROM buytbl
GROUP BY userID;

SELECT userID, SUM(price) FROM buytbl
GROUP BY userID;

SELECT userID, AVG(price) FROM buytbl
GROUP BY userID;
-- 회원별 구매 금액의 평균을 구하시오.
SELECT userID, ROUND(AVG(price)) AS pavg FROM buytbl
GROUP BY userID
HAVING ROUND(AVG(price),1) >100;
SELECT userID, ROUND(AVG(price)) AS pavg FROM buytbl
GROUP BY userID
HAVING pavg >100
ORDER BY pavg DESC;

-- 집계함수
SELECT COUNT(DISTINCT(userID)) FROM buytbl;

-- groupName 별 구매 고객의 수를 구하시오.
SELECT groupName, COUNT(DISTINCT(userID)) FROM buytbl
GROUP BY groupName;

-- usertbl 회원 들의 평균 키보다 큰 회원을 조회 하시오.
SELECT * FROM usertbl
WHERE height > (SELECT AVG(height) FROM usertbl);

-- 회원 중 폰을 가지고 있는 회원수 
SELECT COUNT(mobile1) FROM usertbl;

SELECT userID, groupName, Sum(price*amount) FROM buytbl
GROUP BY userID, groupName
HAVING userID IN('BBK','KBS')
AND groupName IS NOT NULL
ORDER BY userID;

SELECT num,groupName, SUM(price*amount) FROM buytbl
GROUP BY groupName,num
WITH ROLLUP;


-- COMPANYDB
SELECT * FROM emp;

-- 1. 부서별, 직급별 연봉 평균
SELECT deptno,titleno,ROUND(AVG(salary)) AS psalary FROM emp
GROUP BY deptno,titleno
ORDER BY deptno;
-- 2. 입사 년도 별 월급의 평균을 구하시오
SELECT year(hdate), ROUND(AVG(salary))  FROM emp
group by year(hdate)
ORDER BY hdate;

-- 3. 부서 별 입사 월을 기준으로 연봉의 합을 구하시오
SELECT MONTH(hdate), ROUND(AVG(salary)) FROM EMP
GROUP BY MONTH(hdate)
ORDER BY hdate;

-- 4. 이영업이 속한 부서의 연봉의 평균을 구하시오
SELECT deptno, ROUND(AVG(salary)) FROM emp
GROUP BY deptno
HAVING deptno = (SELECT deptno FROM emp
WHERE empname = '이영업');

-- 5. 홍영자 직급과 같은 직원들의 연봉 평균 보다 많이 받는 직원을 구하시오.
SELECT titleno, ROUND(AVG(salary)) FROM EMP
GROUP BY titleno
HAVING titleno = (SELECT titleno FROM emp
WHERE empname = '홍영자');
SELECT * FROM emp
WHERE salary >= 3533;

SELECT empname, salary FROM emp
WHERE salary > (SELECT AVG(salary) FROM emp
WHERE titleno = (SELECT titleno FROM emp
WHERE empname = '홍영자'));

-- 6. 회사내 매니저는 총 몇명인지 구하시오.
SELECT manager, COUNT(manager) FROM emp
GROUP BY manager
WITH ROLLUP;

-- 7. 2000-01-01 부터 2002-12-31일 까지 입사한 직원들의 연봉 평균.
SELECT ROUND(AVG(salary)) FROM emp
WHERE hdate BETWEEN '2000-01-01' AND '2002-12-31';
```





### SQL DML & SELECT

```SQL
-- TABLE 생성

DROP TABLE IF EXISTS itemtbl;
CREATE TABLE itemtbl(
	id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(20) NOT NULL UNIQUE,
    price INT NOT NULL,
    regdate DATE
);

ALTER TABLE itemtbl AUTO_INCREMENT=1000;
INSERT INTO itemtbl VALUES (NULL, 'PANTS1',10000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS2',20000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS3',30000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS4',40000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS5',50000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS6',60000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS7',70000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS8',80000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS9',90000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'PANTS10',100000,SYSDATE());
INSERT INTO itemtbl VALUES (NULL, 'SHIRTS',NULL,SYSDATE());

SELECT * FROM itemtbl;

DROP TABLE IF EXISTS carttbl;
CREATE TABLE carttbl(
	id INT PRIMARY KEY AUTO_INCREMENT,
    userID CHAR(8) NOT NULL,
    itemID INT NOT NULL,
    qt INT NOT NULL,
    regdate DATE
);

INSERT INTO carttbl VALUES(NULL, 'BBK',1000,10,SYSDATE());
INSERT INTO carttbl VALUES(NULL, 'KBS',1001,5,SYSDATE());
INSERT INTO carttbl VALUES(NULL, 'JYP',1004,2,SYSDATE());

SELECT * FROM carttbl;

DELETE FROM carttbl WHERE id = '6';

WITH temp(userID,total)
AS
(SELECT userID, SUM(price*amount) FROM buytbl
GROUP BY userID)
SELECT * FROM temp;

-- 각 지역 별 겨장 키가 큰 키들의 평균을 구하시오.
WITH temp(addr,max)
AS
(SELECT addr, MAX(height) FROM usertbl
GROUP BY addr)
SELECT ROUND(AVG(max)) FROM temp;

SELECT AVG(a.hmax) FROM(
SELECT addr,MAX(height) AS hmax FROM usertbl
GROUP BY addr)a;

SELECT CONCAT(prodName, groupName) FROM buytbl;

SELECT userID, price*amount AS tt, IF (price*amount > 500, 'HEIGHT','LOW') FROM buytbl;

SELECT 	ProdName,IFNULL (groupName,'none') FROM buytbl;
SELECT COUNT(IFNULL (groupName,'none')) FROM buytbl;

SELECT userID,amount,
CASE
	WHEN amount >= 1 AND amount < 2 THEN 'C'
    WHEN amount >= 2 AND amount < 4 THEN 'B'
    WHEN amount >= 4 AND amount < 6 THEN 'A'
	ELSE 'None'
END AS LEVEL
FROM buytbl;

SELECT char_length('abc') , LENGTH('abc');

SELECT mDATE,ADDDATE(mdate, INTERVAL 30 DAY),
	SUBDATE(mDATE , INTERVAL 30 DAY) 
FROM usertbl;

SELECT CURDATE();
SELECT CURTIME();
SELECT NOW();
SELECT SYSDATE();

SELECT DATE_FORMAT (mDATE, '%Y-%m-%d')FROM usertbl;

-- 일수 계산
SELECT mDate, DATEDIFF (mDATE,NOW()) FROM usertbl;
-- 월수 계산.
SELECT mDATE, 
PERIOD_DIFF(DATE_FORMAT(NOW(),'%Y%m'),DATE_FORMAT(mDATE,'%Y%m'))
FROM usertbl;

SELECT * FROM emp;
-- 1.오늘 날짜 기준으로 입사 일부터 며칠이 지났고 몇달이 지났는지 출력하시오
SELECT hdate, DATEDIFF (hdate,NOW()) FROM emp;
SELECT hdate, 
PERIOD_DIFF(DATE_FORMAT(NOW(),'%Y%m'),DATE_FORMAT(hdate,'%Y%m'))
FROM  emp;
-- 2.직원들 연봉이 4000이상이면 high, 2500 이상이면 middle 2500이하면 low 출력alter
SELECT empname, salary,
CASE 
	WHEN salary >= 4000 THEN 'HIGH'
    WHEN salary < 4000 AND salary >= 2500 THEN 'MIDDLE'
    WHEN salary <= 2500 THEN 'LOW'
END AS LEVEL
FROM emp;
-- 3.부서 별 연봉 평균의 합.
SELECT deptno, AVG(salary) FROM emp
GROUP BY deptno;
-- 4.부서 별 입사일 평균을 구하시오
SELECT deptno, Round(AVG(datediff(now(),hdate)),0) AS havg FROM emp
GROUP BY deptno;
-- 5. 이말숙 직원과 같은 해에 입사하는 직원을 조회
SELECT empname, hdate FROM emp
WHERE YEAR(hdate) = (SELECT YEAR(hdate) FROM emp
WHERE empname = '이말숙');
-- 6. 부서별 최고 임금을 받는 직원의 평균을 구하고 그 평균 보다 많이 받는 직원을 조회.
SELECT empname , salary FROM emp
WHERE salary >=(SELECT AVG(a.smax) FROM(
SELECT deptno, MAX(salary) AS smax FROM emp
GROUP BY deptno)a);

-- 1. 입사일이 24년 지난 직원들의 연봉의 평균을 구하시오.
SELECT empname,salary,hdate from emp
WHERE (period_diff(date_format(now(),'%Y%m'),date_format(hdate,'%Y%m')))/12 >= 24;

-- 2. 부서별 입사일이 제일 오래된 직원들 중 연봉이 제일 낮은 사람을 구하시오
SELECT * FROM emp
GROUP BY deptno
HAVING hdate = MIN(hdate);

-- 3. 이말숙 직원보다 늦게 입사한 직원들의 연봉의 합을 구하시오.
SELECT sum(salary) FROM emp
WHERE YEAR(hdate) > (SELECT YEAR(hdate) FROM emp
WHERE empname = '이말숙');

-- 4. 직급별 가장 높은 연봉의 직원들을 구하시오.
SELECT titleno, empname, Max(salary) AS Msalary FROM emp
GROUP BY titleno;

-- 1.연봉이 1000 ~ 3000 사이의 사람들의 정보를 조회하시오
SELECT * FROM emp
WHERE salary >= 1000 AND salary <= 3000;
-- 2.이영업과 매니저가 같은 직원을 조회하여 그 직원들의 연봉 평균을 구하시오.
SELECT manager, AVG(salary) AS avgsalary FROM emp
WHERE manager = (SELECT manager FROM emp
WHERE empname = '이영업'); 
-- 3. 문제 성이 김씨인 직원들의 평균 연봉을 구하고 이들 평균 연봉 보다 낮은 연봉의 직원의 근속일수를 구하시오. (근속일수는 현재-입사일)
SELECT  empname, DATEDIFF (NOW(),hdate) AS wokrDay FROM emp
WHERE salary <= (SELECT AVG(salary) AS avgsalary  FROM emp
WHERE empname LIKE '김%');
-- 4. 이름이 '홍' 과 '이' 로 시작하는 사람들 평균 연봉들을 구하시오
SELECT AVG(salary) AS avgsalary FROM emp
WHERE empname like '이%' OR empname LIKE '홍%';

```

