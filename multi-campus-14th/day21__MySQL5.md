# 📢day21\_\_MySQL workshop

## ERD

![ButcherShop](day21__MySQL5.assets/ButcherShop.png)

### DDL

```sql
-- DDL

DROP DATABASE IF EXISTS butchershopdb;

CREATE DATABASE butchershopdb;
USE butchershopdb;


DROP TABLE IF EXISTS coupon;
DROP TABLE IF EXISTS mycoupon;
DROP TABLE IF EXISTS cust;
DROP TABLE IF EXISTS cate;
DROP TABLE IF EXISTS meat;
DROP TABLE IF EXISTS shipping;
DROP TABLE IF EXISTS payment;
DROP TABLE IF EXISTS ordertbl;
DROP TABLE IF EXISTS detail;
DROP TABLE IF EXISTS cart;


-- coupon table
CREATE TABLE coupon (
	id VARCHAR(30) PRIMARY KEY NOT NULL,
    name VARCHAR(30) NOT NULL,
    saleRate DOUBLE NOT NULL,
    regdate DATE NOT NULL,
    period DATE
);

-- cust table
CREATE TABLE cust(
	id VARCHAR(30) PRIMARY KEY NOT NULL,
	name VARCHAR(30) NOT NULL,
    pwd VARCHAR(30) NOT NULL,
    addr VARCHAR(100) NOT NULL,
    regdate DATE NOT NULL
);

-- mycoupon table
CREATE TABLE mycoupon (
	id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    couponid VARCHAR(30) NOT NULL,
    custid VARCHAR(30)
);
ALTER TABLE mycoupon ADD CONSTRAINT FOREIGN KEY(couponid)
REFERENCES coupon(id);
ALTER TABLE mycoupon ADD CONSTRAINT FOREIGN KEY(custid)
REFERENCES cust(id);


-- cate table
CREATE TABLE cate (
	id INT PRIMARY KEY NOT NULL,
    name VARCHAR(30) NOT NULL,
    pid INT
);
ALTER TABLE cate ADD CONSTRAINT FOREIGN KEY(pid)
REFERENCES cate (id);

-- meat table
CREATE TABLE meat (
	id INT PRIMARY KEY NOT NULL,
    name VARCHAR(30),
    price INT NOT NULL,
    grade CHAR(1) NOT NULL,
    death DATE NOT NULL,
    country VARCHAR(20),
    cateid INT
);
ALTER TABLE meat ADD CONSTRAINT FOREIGN KEY(cateid)
REFERENCES cate(id);
ALTER TABLE meat ADD CONSTRAINT CHECK (price > 0);


-- shipping table
CREATE TABLE shipping (
	shipno INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	addr1 VARCHAR(30) NOT NULL,
    addr2 VARCHAR(30) NOT NULL,
    zip CHAR(5) NOT NULL,
    reciever VARCHAR(20) NOT NULL,
    phone VARCHAR(30) NOT NULL,
    memo VARCHAR(100)
);
ALTER TABLE shipping AUTO_INCREMENT = 1000;

-- payment table
CREATE TABLE payment (
	pno INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    way VARCHAR(30) NOT NULL,
    pdate DATE NOT NULL
);

-- ordertbl table
CREATE TABLE ordertbl (
	num INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	custid VARCHAR(30) ,
    pstatus VARCHAR(20) NOT NULL,
    dstatus VARCHAR(20) NOT NULL,
    regdate DATE NOT NULL,
    mycouponid INT,
    shipno INT,
    pno INT
);
ALTER TABLE ordertbl ADD CONSTRAINT FOREIGN KEY (custid)
REFERENCES cust(id);
ALTER TABLE ordertbl ADD CONSTRAINT FOREIGN KEY (shipno)
REFERENCES shipping(shipno);
ALTER TABLE ordertbl ADD CONSTRAINT FOREIGN KEY (pno)
REFERENCES payment(pno);
ALTER TABLE ordertbl ADD CONSTRAINT FOREIGN KEY(mycouponid)
REFERENCES mycoupon(id);
ALTER TABLE ordertbl AUTO_INCREMENT = 100;

-- detail table
CREATE TABLE detail (
	id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    ordernum INT,
    meatid INT,
    amount INT
);
ALTER TABLE detail ADD CONSTRAINT FOREIGN KEY(ordernum)
REFERENCES ordertbl(num);
ALTER TABLE detail ADD CONSTRAINT FOREIGN KEY(meatid)
REFERENCES meat(id);
ALTER TABLE detail ALTER COLUMN amount SET DEFAULT 10;
ALTER TABLE detail ADD CONSTRAINT CHECK (amount >= 1);


-- cart table
CREATE TABLE cart (
	id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	meatid INT,
    uid VARCHAR(30),
	amount INT
);
ALTER TABLE cart ALTER COLUMN amount SET DEFAULT 10;
ALTER TABLE cart ADD CONSTRAINT FOREIGN KEY(meatid)
REFERENCES meat(id);
ALTER TABLE cart ADD CONSTRAINT FOREIGN KEY(uid)
REFERENCES cust(id);
ALTER TABLE cart ADD CONSTRAINT CHECK (amount >= 1);

```

### DML

```sql
-- coupondata
INSERT INTO coupon VALUES ('coupon1','5%할인쿠폰',0.95,'2022-05-01',null);
INSERT INTO coupon VALUES ('coupon2','15%할인쿠폰',0.85,CURDATE(),'2022-05-30');
SELECT * FROM coupon;

-- custdata
SELECT *FROM cust;
INSERT INTO cust VALUES ('id001','KIM','1234','서울','2021-12-31');
INSERT INTO cust VALUES ('id002','LEE','1234','대전','2022-1-31');

-- mycoupondata
SELECT *FROM mycoupon;
INSERT INTO mycoupon VALUES (NULL,'coupon1','id001');
INSERT INTO mycoupon VALUES (NULL,'coupon2','id002');


-- cate date
INSERT INTO cate VALUES ('100','소',NULL);
INSERT INTO cate VALUES ('200','돼지',NULL);
INSERT INTO cate VALUES ('300','닭',NULL);
INSERT INTO cate VALUES ('310','닭가슴살',300);
INSERT INTO cate VALUES ('390','통탉',300);
INSERT INTO cate VALUES ('110','소 갈비살',100);
INSERT INTO cate VALUES ('120','소 안창살',100);
INSERT INTO cate VALUES ('220','돼지 삼겹살',200);
INSERT INTO cate VALUES ('210','돼지 갈비',200);
INSERT INTO cate VALUES ('230','돼지 앞다리살',200);
SELECT * FROM cate;

-- meat data
INSERT INTO meat VALUES (3112,'하림냉동닭가슴살','700','B','2022-05-01','브라질산','310');
INSERT INTO meat VALUES (3911,'냉장 통닭','6000','A','2022-05-01','국내산','390');
INSERT INTO meat VALUES (1112,'냉장 소 갈비살','9700','A','2022-04-29','미국산','110');
INSERT INTO meat VALUES (1111,'냉장 소 갈비살','14900','A','2022-04-29','국내산','110');
INSERT INTO meat VALUES (2212,'냉동 돼지 삼겹살','3900','B','2022-03-29','미국산','220');
INSERT INTO meat VALUES (2311,'암퇘지 앞다리살','1400','A','2022-04-27','국내산','230');

SELECT * FROM meat;

-- shipping data
INSERT INTO shipping VALUES(
	NULL,
    '서울',
    '도봉구 쌍문동',
    '12345',
    'PARK',
    '010-1234-4567',
    '조심히 와주세요 :)'
);
INSERT INTO shipping VALUES(
	NULL,
    '서울',
    '강남구 대치동',
    '12245',
    'LEE',
    '010-1234-4567',
    NULL
);
SELECT * FROM shipping;

-- payment data
INSERT INTO payment VALUES(NULL,'신용카드',curdate());
INSERT INTO payment VALUES(NULL,'계좌이체',curdate());
SELECT * FROM payment;

-- odertbl data
INSERT INTO ordertbl VALUES(
	NULL,
    'id001',
    '결제 완료',
    '배송전',
    '2022-05-03',
    1,
    1000,
    1
);
INSERT INTO ordertbl VALUES(
	NULL,
    'id002',
    '결제 완료',
    '배송중',
    '2022-05-04',
    2,
    1001,
    2
);
SELECT * FROM ordertbl;

-- detail data
INSERT INTO detail VALUES(NULL,100,3112,5);
INSERT INTO detail VALUES(NULL,100,2212,10);
INSERT INTO detail VALUES(NULL,100,1111,6);
INSERT INTO detail (id,ordernum,meatid) VALUES(NULL,100,1112);
SELECT * FROM detail;

-- cart data
INSERT INTO cart VALUES(null,'3112','id001',200);
SELECT * FROM cart;

-- make view table

-- 주문상세정보 -고객ID,상품명,배송상태,받는사람,양,가격,등급,생산지,totalprice
CREATE VIEW v_detail
AS
SELECT
	ot.custid,
    ot.dstatus,
	m.name,
	d.amount,
    m.price,
    m.grade,
    m.country,
    d.amount * m.price*cp.saleRate AS totalprice
FROM detail d
INNER JOIN meat m ON d.meatid = m.id
INNER JOIN ordertbl ot ON d.ordernum = ot.num
INNER JOIN mycoupon mc on ot.mycouponid = mc.id
INNER JOIN coupon cp on cp.id = mc.couponid;

SELECT * FROM v_detail;


-- v_ordertbl(주문정보) -수신인,받는사람,배송지,우편번호,전화번호,주문날자,배송상태,결제날자,결제상태,총결제금액.
CREATE VIEW v_ordertbl
AS
SELECT
		ot.custid AS 고객아이디,
		s.reciever AS 받는사람,
		s.addr2 AS 받는분주소,
        s.zip AS 우편번호,
        s.phone AS 전화번호,
        ot.regdate 	AS 주문날자,
		ot.dstatus AS 배송상태,
        p.pdate AS 결제날자,
        ot.pstatus AS 결제상태,
		SUM(d.amount * m.price*cp.saleRate) AS 총결제금액
FROM detail d
INNER JOIN meat m ON d.meatid = m.id
INNER JOIN ordertbl ot ON d.ordernum = ot.num
INNER JOIN shipping s ON ot.shipno = s.shipno
INNER JOIN payment p ON ot.pno = p.pno
INNER JOIN cust cu ON ot.custid = cu.id
INNER JOIN mycoupon mc on ot.mycouponid = mc.id
INNER JOIN coupon cp on cp.id = mc.couponid
GROUP BY ot.custid;

SELECT * FROM v_ordertbl;


-- cart view -상품명,등급,도축일,국가,수량,가격
CREATE VIEW v_cart
AS
SELECT
	m.name,
    m.grade,
    m.death,
    m.country,
    car.amount,
    (car.amount*m.price) AS cpirce
FROM cart car
INNER JOIN meat m ON car.meatid = m.id;

SELECT * FROM v_cart;
```
