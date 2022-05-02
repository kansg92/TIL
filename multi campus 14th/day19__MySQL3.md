# 📢 day19__MySQL

### JSON DATA 추출

```SQL
-- JSONDATA 추출 방법.
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
-- 장바구니에 고객이름별 총 금액의 평균을 구하시오.
SELECT cu.name, ROUND(AVG(c.num * i.price)) AS iavg FROM cart c
INNER JOIN cust cu ON c.custid = cu.id
INNER JOIN item i ON c.itemid = i.id
GROUP BY cu.name
HAVING iavg >= 100000;
-- 사원 정보를 출력하시오.
-- 사원번호, 사원이름, 부서명, 직급명 정보 추출.
SELECT t.titleno, e.empname ,d.deptname ,t.titlename  FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
ORDER BY titleno;
-- 각 부서별 평균 연봉 정보 추출.
SELECT d.deptname, AVG(e.salary)FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
GROUP BY d.deptname;
```



### OUTER JOIN

```SQL
-- OUUTER JOIN
-- 어느 한쪽에는 해당 데이타가 있고, 한쪽에는 해당 데이타가 존재하지 않을 때 사용.(많이 사용되진 않음)
SELECT * FROM emp e
RIGHT OUTER JOIN title t ON e.titleno = t.titleno;
SELECT * FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno;
SELECT * FROM emp e
RIGHT OUTER JOIN title t ON e.titleno = t.titleno
UNION
SELECT * FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno;
-- 이름, 부서명, 직급명을 출력. 단 이말자 또한 출력한다.
SELECT e.empname, d.deptname, t.titlename  FROM emp e
LEFT OUTER JOIN title t ON e.titleno = t.titleno
LEFT OUTER JOIN dept d ON e.deptno = d.deptno;
```



### CROSS JOIN

```SQL
-- CROSS JOIN
-- 한테이블의 모든 행들과 다른 테이블의 모든 핸들을 합친다. 쓸일은 없다~
SELECT * FROM emp e
CROSS JOIN title t;
```



### SELF JOIN

```SQL
-- SELF JOIN !중요!
-- 한 테이블에서 데이터값이 중복이 되었을 때 해당 정보를 추출할때 사용.
SELECT * FROM emp;
-- 사원 이름과 매니저 이름을 출력하시오. (e1 = 직원, e2 = 매니저)
SELECT e1.empname,e2.empname FROM emp e1
INNER JOIN emp e2 ON e1.manager = e2.empno;
-- 단, 모든 직원을 같이 출력하시오.
SELECT e1.empname,e2.empname FROM emp e1
LEFT OUTER JOIN emp e2 ON e1.manager = e2.empno;
-- 이름, 부서명, 직급명, 매니저명 을 출력하고, 모든 직원 정보를 출력한다.
SELECT e1.empname,d.deptname,t.titlename,e2.empname AS managerName FROM emp e1
LEFT OUTER JOIN emp e2 ON e1.manager = e2.empno
LEFT OUTER JOIN title t ON e1.titleno = t.titleno
LEFT OUTER JOIN dept d ON e1.deptno = d.deptno;
```



### WORK SHOP

```SQL
-- wokrShop1
SELECT * FROM emp;
-- 1. 직원정보를 출력 한다. 직원의 연봉 정보와 연봉의 세금 정보를 같이 출력 한다. 세금은 10%
SELECT empname,salary,(salary*0.1) AS tax FROM emp;
-- 2. 직원정보 중 2001 이전에 입사 하였고 월급이 4000만원 미만인 직원을 조회
SELECT * FROM emp
WHERE YEAR(hdate) < 2001 
AND salary >= 4000;
-- 3. manager가 있는 직원 중 이름에 '자' 가 들어가 있는 직원정보 조회
SELECT * FROM emp
WHERE empname LIKE '%자%'
AND manager IS NOT NULL;

-- 4. 월급이 2000미만은 '하' 4000미만은 '중' 4000이상은 '고' 를 출력
SELECT empname, salary,
CASE
	WHEN salary >= 4000 THEN '고'
	WHEN salary >= 2000 OR salary < 4000 THEN '중'
	ELSE '하'
END AS LEVEL
FROM emp;

-- 5. 부서 별 월급의 평균을 구하시오단, 평균이 3000 이상인 부서만 출력
SELECT d.deptname, AVG(salary) AS deptAsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptname
HAVING deptAsalary >= 3000;

-- 6. 부서 별 대리와 사원 연봉의 평균을 구하시오 단, 평균이 2500 이상인 부서만 출력
SELECT * FROM title;
SELECT d.deptname, t.titlename ,AVG(salary) AS deptAsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
INNER JOIN title t ON e.titleno = t.titleno
GROUP BY d.deptname, t.titlename
HAVING t.titlename = '사원' OR t.titlename = '대리'
AND deptAsalary >= 2500;

-- 7. 2000년 부터 2002년에 입사한 직원들의월급의 평균을 구하시오
SELECT AVG(salary) FROM emp
WHERE YEAR(hdate) >= 2000 
AND YEAR(hdate) <= 2002;

-- 8. 부서 별 월급의 합의 ranking을 1위부터 조회 하시오
SELECT deptno, SUM(salary) AS sum FROM emp
GROUP by deptno
ORDER BY SUM DESC;
-- 9. 서울에서 근무하는 직원들을 조회 하시오
SELECT empname, deptloc FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
WHERE deptloc = '서울';
-- 10. 이영자가 속한 부서의 직원들을 조회 하시오
SELECT e.empname, d.deptname FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
WHERE d.deptno = ( SELECT e.deptno FROM emp e
WHERE e.empname ='이영자');

-- 11. 김강국의 타이틀과 같은 직원들을 조회 하시오
SELECT e.empname, t.titlename FROM emp e
INNER JOIN title t ON e.titleno = t.titleno
WHERE t.titleno = (SELECT e.titleno FROM emp e
WHERE e.empname ='김강국');

-- WORKSHOP2

-- 1. 2000 년 이후 입사 한 사원들의 정보르 출력사번, 이름, 타이틀, 부서, 지역
SELECT e.empno,e.empname,t.titlename,d.deptname,d.deptloc FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
LEFT OUTER JOIN title t ON e.titleno = t.titleno
WHERE YEAR(hdate) >= 2000;
-- 2. 부서 이름 별 월급의 평균을 구하시오 단, 평균이 3000 이상인 부서만 출력
SELECT d.deptname, AVG(salary) AS dsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptname
having dsalary >= 3000;
-- 3. 대구 지역의 직원들의 평균 연봉을 구하시오
SELECT d.deptloc, AVG(salary) AS locsalary FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
GROUP BY d.deptloc
HAVING deptloc = '대구';
-- 4. 홍영자 직원와 같은 부서 직원들의 근무 월수를 구하시오 
SELECT e.empname, d.deptname,period_diff( DATE_FORMAT(NOW(),'%Y%m'), DATE_FORMAT(e.hdate,'%Y%m') ) AS workMonth FROM emp e
INNER JOIN dept d ON e.deptno = d.deptno
WHERE d.deptno = (SELECT e.deptno FROM emp e
WHERE e.empname = '홍영자');

-- 5. 입사 년수가 가장 많은 직원 순으로 정렬 하여 순위를 정한다. 이름, 부서명, 직위, 년수
SELECT e.empname, d.deptname, t.titlename, e.hdate FROM emp e
LEFT OUTER JOIN dept d ON e.deptno = d.deptno
LEFT OUTER JOIN title t ON e.titleno = t.titleno
ORDER BY e.hdate;
```

