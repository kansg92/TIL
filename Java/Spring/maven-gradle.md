# 🔔Maven 과 Gradle 차이



## 공부하는 이유

스프링 기반 프로젝트를 시작하면서 Maven을 사용해서 배웠다. Maven을 사용하고 나서 프로젝트 구성, 빌드 툴이 무엇인지 대강 이해 할 수 있었고 편리한 의존성에 감사함을 느꼈다. 매번 프로젝트를 만들때 Maven과 Gradle 중 선택하라고 나온다. Gradle이 게속 눈에 밟혔고 최근에는 Gradle의 사용이 점차 늘어가고 있다고한다. 그래서 둘의 차이점과 둘의 기능을 명확하게 공부해보려고 한다.



## Maven



### Maven이란?

- Apache의 이름 아래 2004년 출시.
- Ant를 사용하던 개발자들의 불편함을 해소, 부가기능을 추가하면서 나왔다.
- Apache 라이센스로 배포되는 오픈 소스 소프트웨어이다.
- 수 많은 라이브러리들을 pom을 통해 관리해주는 도구 이다.
- 메이븐의 특징적인 점은 라이브러리들과 연관된 라이브러리들까지 거미줄처럼 모두 연동이 되어 관리가 된다는 점이다.
- 메이븐은 네트워크를 통해 연관된 라이브러리까지 같이 업데이를 해주기 때문에 사용이 편리하다.
- 즉, 빌드를 쉽게 해주며, 개발 가이드라인을 제공하고, 새로운 기능을 쉽게 설치하고 업데이트 할 수 있다.



#### POM - Projcet Object Model

- Maven의 기능을 이용하기 위해 POM.xml이 사용된다.
- POM은 말 그대로 프로젝트 객체 모델의 정보를 담고 있는 파일이다.
- pom.xml에서 주요하게 다루는 기능은 아래와 같다
  - 프로젝트정보 : 프로젝트의 이름, 라이센스 등
  - 빌드 설정: 소스, 리소스, 라이프사이크별 실행한 플로그인 등 빌드와 관련된 설정
  - 빌드 환경 : 사용자 환경 별로 달라질 수 있는 프로파일 정보
  - pom 연관 정보 : 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등



## Gradle



### Gradle이란??

- Ant와 Maven의 장점을 모아서 2012년에 출시.

- Android OS의 빌드 도구로 주요 사용됨.

- Maven을 사용할 수 있는 변환 가능한 컨벤션 프레임 워크

- 멀티 프로젝트에 사용하기 좋음

- Apache Ivy에 기반한 강력한 의존성 관리

- Maven과 Ivy 래파지토리 완전 지원

- 원격 저장소나, pom, Ivy 파일 없이 연결되는 의존성 관리 지원

- Groovy 문법 사용

- 빌드 속도가 Maven에 비해 10 ~ 100배 가량 빠름

- 빌트툴인 Ant Builder와 Groovy 스크립트 기반으로 만들어져 기존 Ant의 역할과 배포 스크립트의 기능을 모두 사용 가능

  ```
  Groovy?
  Groovy는 Java 가상 머신에서 실행되는 스크립트 언어 입니다. Java 가상 머신에서 동작하지만,Java와는 달리 소스 코드를 컴파일 할 필요는 없습니다. Groovy는 스크립트 언어이고, 소스 코드를 그대로 실행합니다. 또한 Java와 호환되고, Java 클래스 파일을 그대로 Groovy 클래스로 사용할 수 있습니다.Java 문법과 유사하여 빌드 처리를 관리할 수 있는 면에서 Gradle은 Java 개발자가 사용하기에 최고의 빌드관리도구이지 않을까 싶습니다.
  출처: https://dev-coco.tistory.com/65 [슬기로운 개발생활😃:티스토리]
  ```

  

  ## Maven VS Gradle

  Maven과 Gradle의 큰 차이는 build에서 차이가 가장 크다.

  

  Gradle이 Maven 보다 좋은점.

  - Gradle이 시기적으로 늦게 나온 만큼 사용성, 성능 등 비교적 뛰어난 스펙을  가지고 있다.
  - Build라는 동적인 요소를 XML로 정의하기에는 어려운 부분이 많다.
    - 설정 내용이 길어지고 가독성이 떨어짐
    - 의존관계가 복잡한 프로젝트 설정하기에 부적절
    - 상속구조를 이용한 멀티 모듈 구현
    - 특정 설정을 소우의 모듈에서 공유하기 위해서는 부모 프로젝트를 생성하여 상속하게 해야함.
  - Gradle은 Groovy를 사용하기 때문에, 동적인 빌드는 Groovy 스크립트로 플로그인을 호출하거나 직접 코드를 짜면 된다.
    - Configuration Injecton 방식을 사용해서 공통 모듈을 상속해서 사용하는 단점을 커버했다.
    - 설정 주입 시 프로젝트 조건을 체크할 수 있어서 프로젝트별로 주입되는 설정을 다르게 할 수 있다.

  

  ###### Maven - pom.xml

  ```xml
  Maven<?xml version="1.0" encoding="UTF-8"?><project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">   <modelVersion>4.0.0</modelVersion>  
      <groupId>com.example</groupId>   
      <artifactId>demo-maven</artifactId>   
      <version>0.0.1-SNAPSHOT</version>   
      <packaging>jar</packaging>   
      <name>demo-maven</name>   
      <description>Demo project for Spring Boot</description>   
      <parent>      
          <groupId>org.springframework.boot</groupId>     
          <artifactId>spring-boot-starter-parent
          </artifactId>      
          <version>1.5.4.RELEASE</version>      
          <relativePath/> <!-- lookup parent from repository -->   </parent>   <properties>      
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>      <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>      <java.version>1.8</java.version>   
      </properties>   
      <dependencies>      
          <dependency>         
              <groupId>org.springframework.boot</groupId>         
              <artifactId>spring-boot-starter</artifactId>      
          </dependency>      
          <dependency>         
              <groupId>org.springframework.boot</groupId>         
              <artifactId>spring-boot-starter-test</artifactId>         
              <scope>test</scope>      
          </dependency>   
      </dependencies>   
      <build>      
          <plugins>         <plugin>            
              <groupId>org.springframework.boot</groupId>            
              <artifactId>spring-boot-maven-plugin</artifactId>         
              </plugin>      
          </plugins>   
      </build>
  </project>
  출처: https://bkim.tistory.com/13 [어쩌다, 블로그:티스토리]
  ```

  

  

  ##### Build.gradle

  ```
  Grad
  lebuildscript {    
  	ext {
      springBootVersion = '1.5.4.RELEASE'
      }
      repositories {
      mavenCentral()
      }
      dependencies {
      classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
      }}
      
      apply plugin: 'java'
      apply plugin: 'idea'
      apply plugin: 'org.springframework.boot'
      
      version = '0.0.1-SNAPSHOT'
      sourceCompatibility = 1.8
      
      repositories {
      	mavenCentral()
      	
      	
      }dependencies {
      
      	compile('org.springframework.boot:spring-boot-starter')    		
      	testCompile('org.springframework.boot:spring-boot-starter-test')}
  출처: https://bkim.tistory.com/13 [어쩌다, 블로그:티스토리]
  ```

  

  ## 결론

  현재 시점에서는 아직 Maven이 Gradle 보다는 많이 사용되어 지고 있다. 아무래도 익숙함이 가장 큰 것 같다. Maven 보다 Gradle이 성능면에서 모두 월등하기 때문이다. 

  Gradle로 언제 현업에서 모든 것이 바뀔 수 도 있기 때문에 Gradle을 이용해서 찍먹이라도 할 수 있어야 할것 같다. Gradle의 Groovy 문법을 배울 수 있도록 해보자.

  추후엔 프로젝트 빌드타임이 비용문제로 이어져 Gradle로 반 강제적으로 바꾸어지는 날이 생길 수 도 있을 것같다.

  항상 새로운 변화를 두려워하지말고 새로운 공부를 할 수 있는 마음가짐을 가지자.

  

  

  

  

  

  #### 참고 자료

  출처: https://bkim.tistory.com/13 [어쩌다, 블로그:티스토리]

  출처: https://dev-coco.tistory.com/65 [슬기로운 개발생활😃:티스토리]

