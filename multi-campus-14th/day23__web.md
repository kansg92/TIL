# 📢day23__WEB&Spring

##### web은 3가지 언어로 구성되어있다.

- HTML
- CSS
- javascript

##### 자바 스프링 설치

1. help -> maketplace 통해서 spring설치가 가능함.

### 자바 스프링 환경셋팅

1. project 생성

2. Spring Boot > Spring Starter Project 선택

3. 프로젝트명 입력

4. Group과 Package 명 선택, 반드시 두개 이상의 package 명으로 입력

5. Dependencies 선택

   1) Spring Boot DevTools

   2) Spring Web

6. pom.xml 추가

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



7. Directory 생성

​	src > main > webapp > WEB-INF > views

8. Proejct Properties > Java Build Path > Source에서 Add Folder

​	WEB-INF > views 선택 추가



9. src/main/resources 에 applications.properties 파일 수정 (반드시 메모장으로 열것)

```
server.port=80
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```



10. 80 port 문제 시 

​	제어판 > 시스템 및 보안 > 관리도구 > 서비스 > World Wide Web Publishibg  서비스 

​	중시 및 수동으로 전환

### Spring

#### (1) 정의

- 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크

