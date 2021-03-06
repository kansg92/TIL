# π’ day19__MySQL

### JSON DATA μΆμΆ

```SQL
-- JSONDATA μΆμΆ λ°©λ².
SELECT JSON_OBJECT('empno',empno,'empname',empname) 
AS JASONDATA
FROM emp;
```

### INNER JOIN

```SQL
-- INNER JOIN.
SELECT c.id, cu.name, i.name, i.price, (c.num * i.price) FROM cart c
INNER JOIN cust cu ON c.custid = cu.id
INNER JOIN item i ON c.itemid = i.id
WHERE i.price > 15000;
-- μ₯λ°κ΅¬λμ κ³ κ°μ΄λ¦λ³ μ΄ κΈμ‘μ νκ· μ κ΅¬νμμ€.
SELECT cu.name, ROUND(AVG(c.num * i.price)) AS iavg FROM cart c
INNER JOIN cust cu ON c.custid = cu.id
INNER JOIN item i ON c.itemid = i.id
GROUP BY cu.name
HAVING iavg >= 100000;
-- μ¬μ μ λ³΄λ₯Ό μΆλ ₯νμμ€.
-- μ¬μλ²νΈ, μ¬μμ΄λ¦, λΆμλͺ, μ§κΈλͺ μ λ³΄ μΆμΆ.
SELECT t.titleno, e.empname ,d.deptname ,t.titlename  FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
ORDER BY titleno;
-- κ° λΆμλ³ νκ·  μ°λ΄ μ λ³΄ μΆμΆ.
SELECT d.deptname, AVG(e.salary)FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
GROUP BY d.deptname;
```



### OUTER JOIN

```SQL
-- OUUTER JOIN
-- μ΄λ νμͺ½μλ ν΄λΉ λ°μ΄νκ° μκ³ , νμͺ½μλ ν΄λΉ λ°μ΄νκ° μ‘΄μ¬νμ§ μμ λ μ¬μ©.(λ§μ΄ μ¬μ©λμ§ μμ)
SELECT * FROM emp e
RIGHT OUTER JOIN title t ON e.titleno = t.titleno;
SELECT * FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno;
SELECT * FROM emp e
RIGHT OUTER JOIN title t ON e.titleno = t.titleno
UNION
SELECT * FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno;
-- μ΄λ¦, λΆμλͺ, μ§κΈλͺμ μΆλ ₯. λ¨ μ΄λ§μ λν μΆλ ₯νλ€.
SELECT e.empname, d.deptname, t.titlename  FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno
LEFT OUTER JOIN dept d ON e.deptno = d.deptno;
```



### CROSS JOIN

```SQL
-- CROSS JOIN
-- ννμ΄λΈμ λͺ¨λ  νλ€κ³Ό λ€λ₯Έ νμ΄λΈμ λͺ¨λ  νΈλ€μ ν©μΉλ€. μΈμΌμ μλ€~
SELECT * FROM emp e
CROSS JOIN title t;
```



### SELF JOIN

```SQL
-- SELF JOIN !μ€μ!
-- ν νμ΄λΈμμ λ°μ΄ν°κ°μ΄ μ€λ³΅μ΄ λμμ λ ν΄λΉ μ λ³΄λ₯Ό μΆμΆν λ μ¬μ©.
SELECT * FROM emp;
-- μ¬μ μ΄λ¦κ³Ό λ§€λμ  μ΄λ¦μ μΆλ ₯νμμ€. (e1 = μ§μ, e2 = λ§€λμ )
SELECT e1.empname,e2.empname FROM emp e1
INNER JOIN emp e2 ON e1.manager = e2.empno;
-- λ¨, λͺ¨λ  μ§μμ κ°μ΄ μΆλ ₯νμμ€.
SELECT e1.empname,e2.empname FROM emp e1
LEFT OUTER JOIN emp e2 ON e1.manager = e2.empno;
-- μ΄λ¦, λΆμλͺ, μ§κΈλͺ, λ§€λμ λͺ μ μΆλ ₯νκ³ , λͺ¨λ  μ§μ μ λ³΄λ₯Ό μΆλ ₯νλ€.
SELECT e1.empname,d.deptname,t.titlename,e2.empname AS managerName FROM emp e1
LEFT OUTER JOIN emp e2 ON e1.manager = e2.empno
LEFT OUTER JOIN title t ON e1.titleno = t.titleno
LEFT OUTER JOIN dept d ON e1.deptno = d.deptno;
```



### WORK SHOP

```SQL
-- wokrShop1
SELECT * FROM emp;
-- 1. μ§μμ λ³΄λ₯Ό μΆλ ₯ νλ€. μ§μμ μ°λ΄ μ λ³΄μ μ°λ΄μ μΈκΈ μ λ³΄λ₯Ό κ°μ΄ μΆλ ₯ νλ€. μΈκΈμ 10%
SELECT empname,salary,(salary*0.1) AS tax FROM emp;
-- 2. μ§μμ λ³΄ μ€ 2001 μ΄μ μ μμ¬ νμκ³  μκΈμ΄ 4000λ§μ λ―Έλ§μΈ μ§μμ μ‘°ν
SELECT * FROM emp
WHERE YEAR(hdate) < 2001 
AND salary >= 4000;
-- 3. managerκ° μλ μ§μ μ€ μ΄λ¦μ 'μ' κ° λ€μ΄κ° μλ μ§μμ λ³΄ μ‘°ν
SELECT * FROM emp
WHERE empname LIKE '%μ%'
AND manager IS NOT NULL;

-- 4. μκΈμ΄ 2000λ―Έλ§μ 'ν' 4000λ―Έλ§μ 'μ€' 4000μ΄μμ 'κ³ ' λ₯Ό μΆλ ₯
SELECT empname, salary,
CASE
	WHEN salary >= 4000 THEN 'κ³ '
	WHEN salary >= 2000 OR salary < 4000 THEN 'μ€'
	ELSE 'ν'
END AS LEVEL
FROM emp;

-- 5. λΆμ λ³ μκΈμ νκ· μ κ΅¬νμμ€λ¨, νκ· μ΄ 3000 μ΄μμΈ λΆμλ§ μΆλ ₯
SELECT d.deptname, AVG(salary) AS deptAsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptname
HAVING deptAsalary >= 3000;

-- 6. λΆμ λ³ λλ¦¬μ μ¬μ μ°λ΄μ νκ· μ κ΅¬νμμ€ λ¨, νκ· μ΄ 2500 μ΄μμΈ λΆμλ§ μΆλ ₯
SELECT * FROM title;
SELECT d.deptname, t.titlename ,AVG(salary) AS deptAsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
GROUP BY d.deptname, t.titlename
HAVING t.titlename = 'μ¬μ' OR t.titlename = 'λλ¦¬'
AND deptAsalary >= 2500;

-- 7. 2000λ λΆν° 2002λμ μμ¬ν μ§μλ€μμκΈμ νκ· μ κ΅¬νμμ€
SELECT AVG(salary) FROM emp
WHERE YEAR(hdate) >= 2000 
AND YEAR(hdate) <= 2002;

-- 8. λΆμ λ³ μκΈμ ν©μ rankingμ 1μλΆν° μ‘°ν νμμ€
SELECT deptno, SUM(salary) AS sum FROM emp
GROUP by deptno
ORDER BY SUM DESC;
-- 9. μμΈμμ κ·Όλ¬΄νλ μ§μλ€μ μ‘°ν νμμ€
SELECT empname, deptloc FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
WHERE deptloc = 'μμΈ';
-- 10. μ΄μμκ° μν λΆμμ μ§μλ€μ μ‘°ν νμμ€
SELECT e.empname, d.deptname FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
WHERE d.deptno = ( SELECT e.deptno FROM emp e
WHERE e.empname ='μ΄μμ');

-- 11. κΉκ°κ΅­μ νμ΄νκ³Ό κ°μ μ§μλ€μ μ‘°ν νμμ€
SELECT e.empname, t.titlename FROM emp e
INNER JOIN title t ON e.titleno = t.titleno
WHERE t.titleno = (SELECT e.titleno FROM emp e
WHERE e.empname ='κΉκ°κ΅­');

-- WORKSHOP2

-- 1. 2000 λ μ΄ν μμ¬ ν μ¬μλ€μ μ λ³΄λ₯΄ μΆλ ₯μ¬λ², μ΄λ¦, νμ΄ν, λΆμ, μ§μ­
SELECT e.empno,e.empname,t.titlename,d.deptname,d.deptloc FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
LEFT OUTER JOIN title t ON e.titleno = t.titleno
WHERE YEAR(hdate) >= 2000;
-- 2. λΆμ μ΄λ¦ λ³ μκΈμ νκ· μ κ΅¬νμμ€ λ¨, νκ· μ΄ 3000 μ΄μμΈ λΆμλ§ μΆλ ₯
SELECT d.deptname, AVG(salary) AS dsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptname
having dsalary >= 3000;
-- 3. λκ΅¬ μ§μ­μ μ§μλ€μ νκ·  μ°λ΄μ κ΅¬νμμ€
SELECT d.deptloc, AVG(salary) AS locsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptloc
HAVING deptloc = 'λκ΅¬';
-- 4. νμμ μ§μμ κ°μ λΆμ μ§μλ€μ κ·Όλ¬΄ μμλ₯Ό κ΅¬νμμ€ 
SELECT e.empname, d.deptname,period_diff( DATE_FORMAT(NOW(),'%Y%m'), DATE_FORMAT(e.hdate,'%Y%m') ) AS workMonth FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
WHERE d.deptno = (SELECT e.deptno FROM emp e
WHERE e.empname = 'νμμ');

-- 5. μμ¬ λμκ° κ°μ₯ λ§μ μ§μ μμΌλ‘ μ λ ¬ νμ¬ μμλ₯Ό μ νλ€. μ΄λ¦, λΆμλͺ, μ§μ, λμ
SELECT e.empname, d.deptname, t.titlename, e.hdate FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
LEFT OUTER JOIN title t ON e.titleno = t.titleno
ORDER BY e.hdate;
```

