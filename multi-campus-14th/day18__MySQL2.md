# π’day18__MySQL2

### SELECT2

```SQL
SELECT * FROM buytbl;

SELECT * FROM buytbl
GROUP BY userID;

SELECT userID, SUM(price) FROM buytbl
GROUP BY userID;

SELECT userID, AVG(price) FROM buytbl
GROUP BY userID;
-- νμλ³ κ΅¬λ§€ κΈμ‘μ νκ· μ κ΅¬νμμ€.
SELECT userID, ROUND(AVG(price)) AS pavg FROM buytbl
GROUP BY userID
HAVING ROUND(AVG(price),1) >100;
SELECT userID, ROUND(AVG(price)) AS pavg FROM buytbl
GROUP BY userID
HAVING pavg >100
ORDER BY pavg DESC;

-- μ§κ³ν¨μ
SELECT COUNT(DISTINCT(userID)) FROM buytbl;

-- groupName λ³ κ΅¬λ§€ κ³ κ°μ μλ₯Ό κ΅¬νμμ€.
SELECT groupName, COUNT(DISTINCT(userID)) FROM buytbl
GROUP BY groupName;

-- usertbl νμ λ€μ νκ·  ν€λ³΄λ€ ν° νμμ μ‘°ν νμμ€.
SELECT * FROM usertbl
WHERE height > (SELECT AVG(height) FROM usertbl);

-- νμ μ€ ν°μ κ°μ§κ³  μλ νμμ 
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

-- 1. λΆμλ³, μ§κΈλ³ μ°λ΄ νκ· 
SELECT deptno,titleno,ROUND(AVG(salary)) AS psalary FROM emp
GROUP BY deptno,titleno
ORDER BY deptno;
-- 2. μμ¬ λλ λ³ μκΈμ νκ· μ κ΅¬νμμ€
SELECT year(hdate), ROUND(AVG(salary))  FROM emp
group by year(hdate)
ORDER BY hdate;

-- 3. λΆμ λ³ μμ¬ μμ κΈ°μ€μΌλ‘ μ°λ΄μ ν©μ κ΅¬νμμ€
SELECT MONTH(hdate), ROUND(AVG(salary)) FROM EMP
GROUP BY MONTH(hdate)
ORDER BY hdate;

-- 4. μ΄μμμ΄ μν λΆμμ μ°λ΄μ νκ· μ κ΅¬νμμ€
SELECT deptno, ROUND(AVG(salary)) FROM emp
GROUP BY deptno
HAVING deptno = (SELECT deptno FROM emp
WHERE empname = 'μ΄μμ');

-- 5. νμμ μ§κΈκ³Ό κ°μ μ§μλ€μ μ°λ΄ νκ·  λ³΄λ€ λ§μ΄ λ°λ μ§μμ κ΅¬νμμ€.
SELECT titleno, ROUND(AVG(salary)) FROM EMP
GROUP BY titleno
HAVING titleno = (SELECT titleno FROM emp
WHERE empname = 'νμμ');
SELECT * FROM emp
WHERE salary >= 3533;

SELECT empname, salary FROM emp
WHERE salary > (SELECT AVG(salary) FROM emp
WHERE titleno = (SELECT titleno FROM emp
WHERE empname = 'νμμ'));

-- 6. νμ¬λ΄ λ§€λμ λ μ΄ λͺλͺμΈμ§ κ΅¬νμμ€.
SELECT manager, COUNT(manager) FROM emp
GROUP BY manager
WITH ROLLUP;

-- 7. 2000-01-01 λΆν° 2002-12-31μΌ κΉμ§ μμ¬ν μ§μλ€μ μ°λ΄ νκ· .
SELECT ROUND(AVG(salary)) FROM emp
WHERE hdate BETWEEN '2000-01-01' AND '2002-12-31';
```





### SQL DML & SELECT

```SQL
-- TABLE μμ±

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

-- κ° μ§μ­ λ³ κ²¨μ₯ ν€κ° ν° ν€λ€μ νκ· μ κ΅¬νμμ€.
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

-- μΌμ κ³μ°
SELECT mDate, DATEDIFF (mDATE,NOW()) FROM usertbl;
-- μμ κ³μ°.
SELECT mDATE, 
PERIOD_DIFF(DATE_FORMAT(NOW(),'%Y%m'),DATE_FORMAT(mDATE,'%Y%m'))
FROM usertbl;

SELECT * FROM emp;
-- 1.μ€λ λ μ§ κΈ°μ€μΌλ‘ μμ¬ μΌλΆν° λ©°μΉ μ΄ μ§λ¬κ³  λͺλ¬μ΄ μ§λ¬λμ§ μΆλ ₯νμμ€
SELECT hdate, DATEDIFF (hdate,NOW()) FROM emp;
SELECT hdate, 
PERIOD_DIFF(DATE_FORMAT(NOW(),'%Y%m'),DATE_FORMAT(hdate,'%Y%m'))
FROM  emp;
-- 2.μ§μλ€ μ°λ΄μ΄ 4000μ΄μμ΄λ©΄ high, 2500 μ΄μμ΄λ©΄ middle 2500μ΄νλ©΄ low μΆλ ₯alter
SELECT empname, salary,
CASE 
	WHEN salary >= 4000 THEN 'HIGH'
    WHEN salary < 4000 AND salary >= 2500 THEN 'MIDDLE'
    WHEN salary <= 2500 THEN 'LOW'
END AS LEVEL
FROM emp;
-- 3.λΆμ λ³ μ°λ΄ νκ· μ ν©.
SELECT deptno, AVG(salary) FROM emp
GROUP BY deptno;
-- 4.λΆμ λ³ μμ¬μΌ νκ· μ κ΅¬νμμ€
SELECT deptno, Round(AVG(datediff(now(),hdate)),0) AS havg FROM emp
GROUP BY deptno;
-- 5. μ΄λ§μ μ§μκ³Ό κ°μ ν΄μ μμ¬νλ μ§μμ μ‘°ν
SELECT empname, hdate FROM emp
WHERE YEAR(hdate) = (SELECT YEAR(hdate) FROM emp
WHERE empname = 'μ΄λ§μ');
-- 6. λΆμλ³ μ΅κ³  μκΈμ λ°λ μ§μμ νκ· μ κ΅¬νκ³  κ·Έ νκ·  λ³΄λ€ λ§μ΄ λ°λ μ§μμ μ‘°ν.
SELECT empname , salary FROM emp
WHERE salary >=(SELECT AVG(a.smax) FROM(
SELECT deptno, MAX(salary) AS smax FROM emp
GROUP BY deptno)a);

-- 1. μμ¬μΌμ΄ 24λ μ§λ μ§μλ€μ μ°λ΄μ νκ· μ κ΅¬νμμ€.
SELECT empname,salary,hdate from emp
WHERE (period_diff(date_format(now(),'%Y%m'),date_format(hdate,'%Y%m')))/12 >= 24;

-- 2. λΆμλ³ μμ¬μΌμ΄ μ μΌ μ€λλ μ§μλ€ μ€ μ°λ΄μ΄ μ μΌ λ?μ μ¬λμ κ΅¬νμμ€
SELECT * FROM emp
GROUP BY deptno
HAVING hdate = MIN(hdate);

-- 3. μ΄λ§μ μ§μλ³΄λ€ λ¦κ² μμ¬ν μ§μλ€μ μ°λ΄μ ν©μ κ΅¬νμμ€.
SELECT sum(salary) FROM emp
WHERE YEAR(hdate) > (SELECT YEAR(hdate) FROM emp
WHERE empname = 'μ΄λ§μ');

-- 4. μ§κΈλ³ κ°μ₯ λμ μ°λ΄μ μ§μλ€μ κ΅¬νμμ€.
SELECT titleno, empname, Max(salary) AS Msalary FROM emp
GROUP BY titleno;

-- 1.μ°λ΄μ΄ 1000 ~ 3000 μ¬μ΄μ μ¬λλ€μ μ λ³΄λ₯Ό μ‘°ννμμ€
SELECT * FROM emp
WHERE salary >= 1000 AND salary <= 3000;
-- 2.μ΄μμκ³Ό λ§€λμ κ° κ°μ μ§μμ μ‘°ννμ¬ κ·Έ μ§μλ€μ μ°λ΄ νκ· μ κ΅¬νμμ€.
SELECT manager, AVG(salary) AS avgsalary FROM emp
WHERE manager = (SELECT manager FROM emp
WHERE empname = 'μ΄μμ'); 
-- 3. λ¬Έμ  μ±μ΄ κΉμ¨μΈ μ§μλ€μ νκ·  μ°λ΄μ κ΅¬νκ³  μ΄λ€ νκ·  μ°λ΄ λ³΄λ€ λ?μ μ°λ΄μ μ§μμ κ·ΌμμΌμλ₯Ό κ΅¬νμμ€. (κ·ΌμμΌμλ νμ¬-μμ¬μΌ)
SELECT  empname, DATEDIFF (NOW(),hdate) AS wokrDay FROM emp
WHERE salary <= (SELECT AVG(salary) AS avgsalary  FROM emp
WHERE empname LIKE 'κΉ%');
-- 4. μ΄λ¦μ΄ 'ν' κ³Ό 'μ΄' λ‘ μμνλ μ¬λλ€ νκ·  μ°λ΄λ€μ κ΅¬νμμ€
SELECT AVG(salary) AS avgsalary FROM emp
WHERE empname like 'μ΄%' OR empname LIKE 'ν%';

```

