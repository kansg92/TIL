# ๐ขday23__WEB&Spring

##### web์ 3๊ฐ์ง ์ธ์ด๋ก ๊ตฌ์ฑ๋์ด์๋ค.

- HTML
- CSS
- javascript

##### ์๋ฐ ์คํ๋ง ์ค์น

1. help -> maketplace ํตํด์ spring์ค์น๊ฐ ๊ฐ๋ฅํจ.

### ์๋ฐ ์คํ๋ง ํ๊ฒฝ์ํ

1. project ์์ฑ

2. Spring Boot > Spring Starter Project ์ ํ

3. ํ๋ก์ ํธ๋ช ์๋ ฅ

4. Group๊ณผ Package ๋ช ์ ํ, ๋ฐ๋์ ๋๊ฐ ์ด์์ package ๋ช์ผ๋ก ์๋ ฅ

5. Dependencies ์ ํ

   1) Spring Boot DevTools

   2) Spring Web

6. pom.xml ์ถ๊ฐ

        ```html
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



7. Directory ์์ฑ

โ	src > main > webapp > WEB-INF > views

8. Proejct Properties > Java Build Path > Source์์ Add Folder

โ	WEB-INF > views ์ ํ ์ถ๊ฐ



9. src/main/resources ์ applications.properties ํ์ผ ์์  (๋ฐ๋์ ๋ฉ๋ชจ์ฅ์ผ๋ก ์ด๊ฒ)

```
server.port=80
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```



10. 80 port ๋ฌธ์  ์ 

โ	์ ์ดํ > ์์คํ ๋ฐ ๋ณด์ > ๊ด๋ฆฌ๋๊ตฌ > ์๋น์ค > World Wide Web Publishibg  ์๋น์ค 

โ	์ค์ ๋ฐ ์๋์ผ๋ก ์ ํ

### Spring

#### (1) ์ ์

- ์๋ฐ ์ํฐํ๋ผ์ด์ฆ ๊ฐ๋ฐ์ ํธํ๊ฒ ํด์ฃผ๋ ์คํ์์ค ๊ฒฝ๋๊ธ ์ ํ๋ฆฌ์ผ์ด์ ํ๋ ์์ํฌ

