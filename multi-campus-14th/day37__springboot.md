# ๐ขday37__SpringBoot

## Spring Boot web ํ๊ฒฝ์ํ

#### 1. Spring Starter Project ์์ฑ

#### 2. Group, Package ๋ช ์ ํ. ๋ฐ๋์ 2๊ฐ ์ด์์ package ๋ช์ผ๋ก ์๋ ฅ

#### 3. Dependencies ์ ํ

#### 4. pom.xml dependencies ์ถ๊ฐ

```xml
  <!-- @Inject -->
		<dependency>
			<groupId>javax.inject</groupId>
			<artifactId>javax.inject</artifactId>
			<version>1</version>
		</dependency>
		<!-- Servlet -->

		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>


		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>3.0.1</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
		
		<!-- json request -->   

		<dependency>
			<groupId>com.googlecode.json-simple</groupId>
			<artifactId>json-simple</artifactId>
			<version>1.1</version>
  		</dependency>
```



#### 5. Directoy ์์ฑ

- **JSP** 
  - src > main > webapp > WEB-INF > views
  - Java Buid Path > viewsํด๋ ์ถ๊ฐํ์ฌ ๊ด๋ฆฌ.

- **THYMLEAF**
  - templayes์์ htmlํ์ผ ๊ด๋ฆฌ.

### 6. applicaton.properties ํ์ผ ๊ด๋ฆฌ (JSP)

```properties
server.port=80
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```

**thymleaf ์ฌ์ฉ์ ์๋ ํ๊ฒฝ์ํ**

#### 7. spring mysql ํ๊ฒฝ์ํ

1. **dependency SQL ํธ์ถ**
2. **application.porperties ํ์ผ ์ํ**

```properties
server.port=80

spring.datasource.driverClassName=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/shopdb?serverTimezone=Asia/Seoul

spring.datasource.username=admin1
spring.datasource.password=111111

mybatis.type-aliases-package=com.multi.vo
mybatis.mapper-locations=com/multi/mybatis/*.xml
```



#### 80 port ๋ฌธ์  ์

**์ ์ดํ > ์์คํ ๋ฐ ๋ณด์ > ๊ด๋ฆฌ๋๊ตฌ > ์๋น์ค > World Wide Web Publishibg  ์๋น์ค ์ค์ง ๋ฐ ์๋์ผ๋ก ์ ํ**





## THYMLEAF

### thymleaf ๋ฐ๋ณต๋ฌธ (foreach)

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>Cust Select Page</h1>
	<h3><a href="custadd">Cust ADD</a></h3>
	<h3><a href="/">Main</a></h3>
	<table>
		<thead>
			<tr><td>ID</td><td>Name</td></tr>
		</thead>
		<tbody>
			<tr th:each = "c:${allcust}">
				<td th:text ="${c.id}"></td><td th:text ="${c.name}"></td>
			</tr>
		</tbody>
	</table>
	
</body>
</html>
```

