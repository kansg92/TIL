# π’day56__centOS λͺλ Ήμ΄.

## **CentOS λͺλ Ήμ΄ μ λ¦¬**

πν¬νΈ ν¬μλ©μ IPμ ν¬νΈλ  puttyμμ μ²μ μΈνν λλ§ μ¬μ©νλ€.

πμΆν μλ²λ₯Ό μ¬μ©ν  λλ κ³΅μΈIPλ₯Ό μ΄μ©νμ¬ μ μνλ€

### **μλμμ± Tap**

****

#### **viνΈμ§κΈ° μ€ν**

- vi test.txt 

- test.txt νμΌμ΄ μμΌλ©΄ μ€νλκ³ , μμΌλ©΄ μλ‘ λ§λ€μ΄μ μ€νλλ€.

- [vi λͺλ Ήμ΄](https://www.notion.so/96d921122e3f4fd2b36064e3b0d2353a)

- w : write

- q : quit

****

#### **νμΌ λ΄μ© νμΈ**

- `cat  "νμΌ μ΄λ¦.νμΌνμ"`

****

#### **νμΌ λ° λλ ν λ¦¬**

****

#### **λλ ν λ¦¬ λ³κ²½**

- \# μ λ ν¨μ€
  - `cd /home/student `

- \# μλ ν¨μ€
  - `cd../home/student `

- \# νμ¬ μμ λλ ν λ¦¬μ μμΉμ μκ΄μμ΄ ν λλ ν λ¦¬λ‘ μ΄λ
  - `cd  `



****

#### **νμ¬ μμ λλ ν λ¦¬ μ λ ν¨μ€λ‘ μΆλ ₯**

- `pwd`

****

### **λλ ν λ¦¬ νμΌλͺ©λ‘ μΆλ ₯**



##### \# κ°λ΅ν λ³΄κΈ°

- `ls "λλ ν λ¦¬λͺ"`

##### \# μμΈν λ³΄κΈ°

- `ls -l `

##### \# μ¨κΉνμΌ λ³΄κΈ°(.μΌλ‘ μμνλ νμΌ)

- `ls -a `

##### \# μ¨κΉνμΌκΉμ§ μμΈν λ³΄κΈ°

- `ls -al  `



-al λ‘ νμλλ νμΌμ

νμΌ μ’λ₯, μ κ·ΌκΆν, λ§ν¬μ, μμ μ, μμ κ·Έλ£Ή, νμΌν¬κΈ°, λ§μ§λ§ μμ μΌμ, μ¨κΉνμΌλ± μΌλ‘ λμ¨λ€.



[νμΌ μ’λ₯](https://www.notion.so/0b1699b0b7b6437f891e216e2c25c860)

#### **λλ ν λ¦¬ μμ± λ° μ­μ **

##### \# μμ±

- `mkdir  "λλ ν λ¦¬ μ΄λ¦"`

##### \# μ­μ  - λλ ν λ¦¬ μμ λ€λ₯Έ νμΌμ΄λ λλ ν λ¦¬κ° μ‘΄μ¬νμ§ μμμΌλ§ κ°λ₯ 

- `rmdir "λλ ν λ¦¬ μ΄λ¦"`

****

****

#### **νμΌ λ³΅μ¬, μ­μ , νμΌ λ° λλ ν λ¦¬ μ΄λ**

##### \# λ³΅μ¬

- `cp  "νμΌλͺ.νμ₯μ"  "(λ³΅μ¬ν)νμΌλͺ.νμ₯μ" `

##### \# μ­μ 

- `rm  "νμΌλͺ.νμ₯μ"`

##### \# μ΄λ

- `mv  "νμΌλͺ.νμ₯μ"  "μ΄λν  κ²½λ‘`

##### "/"(λ³κ²½κ°λ₯)νμΌλͺ.νμ₯μ"

- `mv "μ΄λν  λμ"  "λλ ν λ¦¬ μ΄λ¦"`



##### \# μ΄λν  λμμ μ΄λ¦μ κ·Έλλ‘ μ μ§****

****

**file μ’λ₯ νμ**

`file λμνμΌκ²½λ‘(νΉμ νμΌκ²½λ‘ν¨ν΄)`

****

**νμΌ μ°ΎκΈ°**

`find κ²μμμμμΉ -name "νμΌλͺν¨ν΄"# νΉμ  νμΌλͺ ν¨ν΄μ κ°λ νμΌλ€μ κ²μν΄μ μ§μ°κΈ°find κ²μμμμμΉ -name "νμΌλͺν¨ν΄" -delete`

****

**νμΌ λ΄λ €λ°κΈ°**

`wget λ€μ΄λ‘λURL `

μ΄μνκ² μ μ₯λλ κ²½μ°κ° μμ΄μ λ€μ λͺλ Ήμ΄ μ¬μ© λ§μ΄ν¨

**λ€λ₯Έ μ΄λ¦μΌλ‘ μ μ₯νκΈ°**

`wget -O μ μ₯λ  νμΌμ΄λ¦ λ€μ΄λ‘λURL`

**μ΄μ΄λ°κΈ°**

`wget -c λ€μ΄λ‘λURL`

**μμΆνκΈ°**

`tar zcvf μμ±λ μμΆνμΌμ΄λ¦ μμΆν μλ³ΈνμΌ_νΉμ_λλ ν λ¦¬`

**ν΄μ νκΈ°**

`tar zxvf μμΆνμΌ_μ΄λ¦`

```
c : μλ‘μ΄ λ¬Άμ λ§λ¬

x : λ¬ΆμΈ νμΌ νμ΄μ€

f : λ¬Άμ νμΌμ μ΄λ¦ μ§μ  μ΅μ

v : λ¬Άμ νμΌμ νκ±°λ λ¬Άμ λ κ³Όμ μ νλ©΄μ μΆλ ₯
```



**zip λͺλ Ήμ΄ μμΆ/ν΄μ **

`zip μμΆνμΌμ΄λ¦ μμΆλμνμΌμ΄λ¦ `

`unzip νμΌμ΄λ¦`

`gzip λͺλ Ήμ΄μ λ¬λ¦¬ λ¬Άμ νμΌμ κ±°μΉμ§ μκ³  λ°λ‘ μμΆ/ν΄μ  κ°λ₯`



### PC νμΌ μ μ‘ μμΆ ν΄μ 



#### 1. λͺλ Ήνλ‘¬ν¬νΈ μ€ν ν λλ ν λ¦¬λ₯Ό zip ννλ‘ λ¬Άμ νμΌ μ μ‘

`scp -P 65000(μΈλΆν¬νΈλ²νΈ) a.zip(νμΌμ΄λ¦) root@101.101.167.122(κ³΅μΈIP):/root(μ μ‘ν  μμΉ)`

#### 2. CentOS μ μ ν μμΆ ν΄μ 

`unzip a.zip`

****



## μλ°μ€μΉ

`# yum list java*jdk-devel`

```
yum  list  java*jdk-devel
yum install  java-1.8.0-openjdk-devel.x86_64

java -version
```



## MySQL μ€μΉ



### Install

```
1) yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm
μ€μΉνμΌ λ€μ΄λ‘λ

2) yum repolist enabled | grep "mysql.*"
λ€μ΄λ°μ νμΌ νμΈ

3) yum install -y mysql-server
μ€μΉ

4) mysql -V
μ€μΉλ²μ  νμΈ
```



### Configuring Server



#### 1) Start & Stop

```ce
systemctl enable mysqld # μ¬λΆν μ μλ μμνλλ‘ μ€μ 
systemctl start mysqld # μλΉμ€ μμ
systemctl status mysqld # μλΉμ€ κ΅¬λ μ¬λΆ νμΈ
```



#### 2) Settings root password

```
grep "temporary password" /var/log/mysqld.log
```



#### 3) rootλ‘ μ μ ν λΉλ° λ²νΈ λ³κ²½(λ°λμ μλ¬Έλμ,μ«μ,νΉμλ¬Έμ)

```
mysql -u root -p

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'λ³κ²½ν  λΉλ°λ²νΈ';
mysql> exit
```



#### 4) λΉλ° μ μ± λ³κ²½

```
mysql -u root -p

mysql> SHOW VARIABLES LIKE 'validate_password%';
mysql> SET GLOBAL validate_password.length = 5; # λ€μ―μλ¦¬κΉμ§λ§..
mysql> SET GLOBAL validate_password.number_count = 0; # μ«μ νμμμ
mysql> SET GLOBAL validate_password.policy=LOW; # μ μ± μμ€μ λ?κ²..
mysql> SET GLOBAL validate_password.mixed_case_count = 0; # λμλ¬Έμ νμμμ
mysql> SET GLOBAL validate_password.special_char_count = 0; # νΉμλ¬Έμ νμμμ
```



#### 5) μ¬μ©μ μμ± λ° λ°μ΄ν°λ² μ΄μ€ μμ±

```
mysql -u root -p

mysql> use mysql;
mysql> select host, user from user;

mysql> CREATE USER 'μμ΄λ'@'%' identified by 'λΉλ°λ²νΈ'; # μΈλΆμ μλ§ κ°λ₯ν κ³μ  μμ±
mysql> CREATE DATABASE DBμ΄λ¦ default character set utf8;
mysql> GRANT ALL PRIVILEGES ON DBμ΄λ¦.* to 'μμ΄λ'@'%'; # ν΄λΉ DBμ λν κΆν λΆμ¬
mysql> flush privileges; # μλ‘κ³ μΉ¨ λ­!
mysql> select host,user from user; # λ€μ νμΈ
```

