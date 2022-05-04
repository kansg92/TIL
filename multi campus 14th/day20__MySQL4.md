# 📢day20__MySQL

#### 📍CMD MYSQL명령

1. mysql -u 유저명 -p  : MySQL접속.
2. SHOW DATABASES;
3. SHOW TABLES;
4. USE database명;
5. DESC TABLE명;



#### 📍제약조건

- 제약조건은 테이블을 먼저 설계하고 나중에 `ALTER`문을 통해서  제약조건을 추가적으로 만드는 것이 좋다.



#### 📍VIEW

1. 복잡한 쿼리를 단순화 시킬 수 있다.
2. 보안성이 강화된다.



### SQL DDL

```sql
-- DDL

DROP DATABASE IF EXISTS shoppingdb;

CREATE DATABASE shoppingdb;
USE shoppingdb;

DROP TABLE IF EXISTS cart;
DROP TABLE IF EXISTS cust;
DROP TABLE IF EXISTS product;
DROP TABLE IF EXISTS cate;

-- CUST TABLE
CREATE TABLE cust(
	id VARCHAR(10) NOT NULL,
    name VARCHAR(20) NOT NULL,
    addr VARCHAR(100) NOT NULL,
    regdate DATE
);
ALTER TABLE cust ADD CONSTRAINT PRIMARY KEY(id);
-- SET DEFAULT
ALTER TABLE CUST ALTER COLUMN addr SET DEFAULT 'Seoul';

-- CATE TABLE
CREATE TABLE cate(
	id INT NOT NULL,
    name VARCHAR(30) NOT NULL,
    pid INT
);
ALTER TABLE cate ADD CONSTRAINT PRIMARY KEY(id);
	-- SET UNIQUE
ALTER TABLE cate ADD CONSTRAINT UNIQUE(name);
	-- set foreign key
ALTER TABLE cate ADD CONSTRAINT FOREIGN KEY(pid)
REFERENCES cate (id);

	-- modify table
-- ALTER TABLE cate CHANGE COLUMN name name VARCHAR(30) NOT NULL;

-- PRODUCT TABLE
CREATE TABLE product(
	id INT,
    name VARCHAR(20) NOT NULL,
    price int NOT NULL,
    regdate DATE NOT NULL,
    cid INT
);
ALTER TABLE product ADD CONSTRAINT PRIMARY KEY(id);
ALTER TABLE product MODIFY id INT NOT NULL AUTO_INCREMENT;
ALTER TABLE product AUTO_INCREMENT = 1000;
ALTER TABLE product ADD CONSTRAINT FOREIGN KEY (cid)
REFERENCES cate(id);
ALTER TABLE product ADD CONSTRAINT CHECK (price > 0 );

-- CART TABLE and COMSTRAINT CREATE
CREATE TABLE cart(
	id INT,
    uid VARCHAR(10),
    pid INT,
    regdate DATE
);
ALTER TABLE cart MODIFY id INT NOT NULL AUTO_INCREMENT PRIMARY KEY FIRST;
ALTER TABLE cart AUTO_INCREMENT = 1000;

ALTER TABLE cart ADD FOREIGN KEY (uid)
REFERENCES cust(id)
	-- ON UPDATE 허용.
ON DELETE CASCADE
ON UPDATE CASCADE;
ALTER TABLE cart ADD FOREIGN KEY (pid)
REFERENCES product(id);
```



### SQL DML

```sql
-- cust data
INSERT INTO cust VALUES ('id01','lee','Busan','2019-03-02');
INSERT INTO cust (id,name,regdate) VALUES ('id02','kim','2020-05-02');
SELECT * FROM cust;

-- cate data
SELECT * FROM cate;
INSERT INTO cate VALUES (10,'pants',NULL);
INSERT INTO cate VALUES (11,'short pants',10);
INSERT INTO cate VALUES (20,'shirts',NULL);
INSERT INTO cate VALUES (21,'short shirts',20);

SELECT * FROM cate c1
INNER JOIN cate c2 ON c1.pid = c2.id;

-- product data
SELECT * FROM product;
INSERT INTO product VALUES (NULL, 'levis', 10000, curdate(),11);
INSERT INTO product VALUES (NULL, 'bang', 20000, curdate(),11);
INSERT INTO product VALUES (NULL, 'levis', 20000, curdate(),21);
INSERT INTO product VALUES (NULL, 'bang', 5000, curdate(),21);

-- 제품의 정보를 출력한다.단, 카데코리 명도 같이 출력.
SELECT p.name, p.price, c.name, p.regdate FROM product p
INNER JOIN cate c ON p.cid = c.id;

-- cart date
SELECT * FROM cart;
INSERT INTO cart VALUES (NULL, 'id01' , 1000, CURDATE());
INSERT INTO cart VALUES (NULL, 'id01' , 1001, CURDATE());
INSERT INTO cart VALUES (NULL, 'id01' , 1003, CURDATE());

-- cart정보를 출력하시오, 사용자 이름, 상품 이름,가격, 카데코리 이름 출력
SELECT cu.name AS username  , p.name AS productname, p.price, cat.name AS category FROM cart ca
INNER JOIN product p ON p.id = ca.pid
INNER JOIN cate cat ON p.cid = cat.id
INNER JOIN cust cu ON cu.id = ca.uid;

SELECT ca.id, cu.id AS uid, cu.name AS uname, cat.name AS cname,p.id AS pid, p.name AS pname, p.price, ca.regdate FROM cart ca
INNER JOIN product p ON p.id = ca.pid
INNER JOIN cate cat ON p.cid = cat.id
INNER JOIN cust cu ON cu.id = ca.uid;

-- VIEW !! 매우 중요 !!
-- MAKE VIEW TABLE
CREATE VIEW v_cart
AS
SELECT ca.id, cu.id AS uid, cu.name AS uname, cat.name AS cname,p.id AS pid, p.name AS pname, p.price, ca.regdate FROM cart ca
INNER JOIN product p ON p.id = ca.pid
INNER JOIN cate cat ON p.cid = cat.id
INNER JOIN cust cu ON cu.id = ca.uid;

-- UPDATE VIEW TABLE 하면 기존 table정보도 update가 같이 된다. 단, 집계함수 또는 UNION을 통해 만들어진 것은 수정이안된다.
UPDATE cart SET regdate ='2020-05-02' WHERE id = 1000;
SELECT * FROM v_cart;
UPDATE v_cart SET regdate ='2019-05-05' WHERE id = 1001;
SELECT * FROM v_cart
WHERE uid = 'id01';

-- DELETE FROM cart;
-- DELETE FROM cust WHERE id = 'id001';
-- UPDATE cust SET id = 'id001' WHERE id ='id01';
```

