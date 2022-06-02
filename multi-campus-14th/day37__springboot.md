# 📢day37__SpringBoot

## Spring Boot web 환경셋팅

#### 1. Spring Starter Project 생성

#### 2. Group, Package 명 선택. 반드시 2개 이상의 package 명으로 입력

#### 3. Dependencies 선택

#### 4. pom.xml dependencies 추가

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



#### 5. Directoy 생성

- **JSP** 
  - src > main > webapp > WEB-INF > views
  - Java Buid Path > views폴더 추가하여 관리.

- **THYMLEAF**
  - templayes에서 html파일 관리.

### 6. applicaton.properties 파일 관리 (JSP)

```properties
server.port=80
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```

**thymleaf 사용시 아래 환경셋팅**

#### 7. spring mysql 환경셋팅

1. **dependency SQL 호출**
2. **application.porperties 파일 셋팅**

```properties
server.port=80

spring.datasource.driverClassName=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/shopdb?serverTimezone=Asia/Seoul

spring.datasource.username=admin1
spring.datasource.password=111111

mybatis.type-aliases-package=com.multi.vo
mybatis.mapper-locations=com/multi/mybatis/*.xml
```



#### 80 port 문제 시

**제어판 > 시스템 및 보안 > 관리도구 > 서비스 > World Wide Web Publishibg  서비스 중지 및 수동으로 전환**





## THYMLEAF

### thymleaf 반복문 (foreach)

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

