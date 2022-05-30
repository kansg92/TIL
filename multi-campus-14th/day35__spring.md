# 📢day35__Spring



## Spring

### Spring, SpringBoot

스프링과 스프링부트는 엄연히 다르다. 스프링은 스프링부트의 전신이며 사용하려면 굉장히 복잡하고 어려운 셋팅들을 해야하기 때문에  프로젝트할때는 스프링부트를 이용해서 작업을 진행할 예정이며, 스프링에대한 개념도 잡고 넘어갈 계획이다.

Spring을 아는것은 DI,AOP적 관점을 알아야한다. 

spring으로 웹을 구성하기 위해서는 Spring MVC 혹은 SpringBoot를 활용해서 만들 수 가 있다.

DI,AOP,SpringMVC,SpringBoot총 4가지 방식이 있으며

DI,AOP경우 XML OR Anotation을 활용하여 할수 있으며, XML로 처리시 양이 많아지면 XML에서 모든걸 컨트롤하기 때문에 XML을 관리하기 어려워질 수 가 있다.



---

## 💡DI(Dependency Injecton) Spring

### 1.Spring XML을 활용하여 처리하기(DI:Dependency Injecton)

#### (1) interface pakage(FRAME)

- 확장성을 위해 인터페이스를 활용하여 frame을 만들어놓고 하자. 자바의 큰 장점이다! OOP!!

##### 1. DAO

```java
package com.frame;

import java.util.List;

public interface Dao<K,V> {	
	
	public void insert(V v);
	public void delete(K k);
	public void update(V v);
	public V select(K k);
	public List<V> select();
}

```

##### 2. Service

```java
package com.frame;

import java.util.List;

public interface Service<K,V> {
	public void register(V v);
	public void remove(K k);
	public void modify(V v);
	public V get(K k);
	public List<V> get();
	
}
```

#### (2) VO

````java
package com.vo;

public class UserVO {
	private String id;
	private String pwd;
	private String name;
	
	public UserVO() {
		
	}

	public UserVO(String id, String pwd, String name) {
		this.id = id;
		this.pwd = pwd;
		this.name = name;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getPwd() {
		return pwd;
	}

	public void setPwd(String pwd) {
		this.pwd = pwd;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return "UsesrVO [id=" + id + ", pwd=" + pwd + ", name=" + name + "]";
	}
	
	
	
````

#### (3) Dao, Service class

##### 1. userDAO

```java
package com.user;

import java.util.ArrayList;
import java.util.List;

import com.frame.Dao;
import com.vo.UserVO;

public class UserDao implements Dao<String, UserVO> {

	
	@Override
	public void insert(UserVO v) {
		System.out.println("Inserted: " +v);
		
	}

	@Override
	public void delete(String k) {
		System.out.println("Deleted: " +k);		
	}

	@Override
	public void update(UserVO v) {
		System.out.println("Updated: " +v);
		
	}

	@Override
	public UserVO select(String k) {
		UserVO user = new UserVO(k,"pwd02","kim");
		return user;
	}

	@Override
	public List<UserVO> select() {
		ArrayList<UserVO> list = new ArrayList<UserVO>();
		list.add(new UserVO("id01", "pwd01", "lee"));
		list.add(new UserVO("id02", "pwd02", "kim"));
		list.add(new UserVO("id03", "pwd03", "park"));
		list.add(new UserVO("id04", "pwd04", "kan"));
		list.add(new UserVO("id05", "pwd05", "yoon"));
		return list;
	}
	
	
}

```

##### 2. userService

```java
package com.user;

import java.util.List;

import com.frame.Dao;
import com.frame.Service;
import com.vo.UserVO;

public class UserService implements Service<String, UserVO> {

	Dao<String, UserVO> dao;
	
	
	
	public Dao<String, UserVO> getDao() {
		return dao;
	}

	public void setDao(Dao<String, UserVO> dao) {
		this.dao = dao;
	}

	@Override
	public void register(UserVO v) {
		dao.insert(v);
	}

	@Override
	public void remove(String k) {
		dao.delete(k);
	}

	@Override
	public void modify(UserVO v) {
		dao.update(v);
	}

	@Override
	public UserVO get(String k) {
		
		return dao.select(k);
	}

	@Override
	public List<UserVO> get() {
		
		return dao.select();
	}

}

```

#### (4) TEST

- 항상 모든기능은 하나씩 TEST를 통해 검증하는 작업이 필요하다.
- TEST작업은 가장 중요한 작업중 하나로 절대로 귀찮아 하지말자. 나중에 꼬여버리는것을 방지할 수 있다.

```java
package com.test;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.frame.Service;
import com.vo.UserVO;

public class UserInsertTest {

	public static void main(String[] args) {
		ApplicationContext factory =
		new ClassPathXmlApplicationContext("spring.xml");
		
		Service<String, UserVO> service = 
				(Service<String, UserVO>) factory.getBean("uservice");
		
		UserVO u = new UserVO("id01","pwd01", "lee");
		service.register(u);
		
	}

}

```

#### (5) XML파일

XML 파일통해서 IOC, DI를 구현하여 사용한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

	<bean id="udao" class="com.user.UserDao"></bean>
    <bean id="uservice" class="com.user.UserService">
    	<property name="dao" ref="udao"></property>
    </bean>
    
   	<bean id="itemdao" class="com.item.ItemDao"></bean>
    <bean id="itemservice" class="com.item.ItemService">
    	<property name="dao" ref="itemdao"></property> <!-- setter 를 이용한 주입. -->
    </bean>
    
   	<bean id="pdao" class="com.product.ProductDao"></bean>
    <bean id="pservice" class="com.product.ProductService">
  	 	<constructor-arg name="dao" ref="pdao"/> <!-- constructor 를 이용한 주입. -->
    </bean>
       
</beans>
```



---

### 2. Anotation 을 활용하여 Spring 구성하기 (DI:Dependency Injection)



#### (1)XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:context="http://www.springframework.org/schema/context" 
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context-3.0.xsd
       ">
	<context:component-scan base-package="com.*"/>
 	
 	
</beans>

```



#### (2)Dao.Service class

##### 1. userDao

- @Repository를 이용해 dao형성

```java
package com.user;

import java.util.ArrayList;
import java.util.List;

import org.springframework.stereotype.Repository;

import com.frame.Dao;
import com.vo.UserVO;

@Repository("userDao")
public class UserDao implements Dao<String, UserVO> {

	
	@Override
	public void insert(UserVO v) {
		System.out.println("Inserted: " +v);
		
	}

	@Override
	public void delete(String k) {
		System.out.println("Deleted: " +k);		
	}

	@Override
	public void update(UserVO v) {
		System.out.println("Updated: " +v);
		
	}

	@Override
	public UserVO select(String k) {
		UserVO user = new UserVO(k,"pwd02","kim");
		return user;
	}

	@Override
	public List<UserVO> select() {
		ArrayList<UserVO> list = new ArrayList<UserVO>();
		list.add(new UserVO("id01", "pwd01", "lee"));
		list.add(new UserVO("id02", "pwd02", "kim"));
		list.add(new UserVO("id03", "pwd03", "park"));
		list.add(new UserVO("id04", "pwd04", "kan"));
		list.add(new UserVO("id05", "pwd05", "yoon"));
		return list;
	}
	
	
}

```

##### 2.userService

- `@service`를 활용해  uservice 형성
- `@Autowired` 를 활용하여 dao에대한것을 검색하여 이름 설정을 해줌.

```java
package com.user; 

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Dao;
import com.frame.Service;
import com.vo.UserVO;

@org.springframework.stereotype.Service("uservice")
public class UserService implements Service<String, UserVO> {
	
	@Autowired //자동으로 dao에대한것을 검색해서 가져오라는 뜻.
	Dao<String, UserVO> dao;
	

	@Override
	public void register(UserVO v) {
		dao.insert(v);
	}

	@Override
	public void remove(String k) {
		dao.delete(k);
	}

	@Override
	public void modify(UserVO v) {
		dao.update(v);
	}

	@Override
	public UserVO get(String k) {
		
		return dao.select(k);
	}

	@Override
	public List<UserVO> get() {
		
		return dao.select();
	}

}
```





## 💡AOP(Aspect Orinted Programming) Spring

보안상으로 만들어진 개념으로 함수가 실핼될 때 마다 보안코드를 모든 클래스에 한번에 적용하기위해 만들어진 개념이다. 하나의 클래스를 연동하여 보안의 유지보수를 편하게 해준다.

### 1. XML을 활용하여 AOP처리하기.

#### (1) XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:context="http://www.springframework.org/schema/context" 
       xmlns:aop="http://www.springframework.org/schema/aop" 
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context-3.0.xsd
       http://www.springframework.org/schema/aop 
       http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
       ">
	<context:component-scan base-package="com.*"/>
 	
 	<bean id="logAdvice" class="com.frame.LoggerAdvice"/>
 	
	<aop:config>
		<!-- com.user 밑에있는 모든 함수, 클래스에 적용.  -->
		<aop:pointcut expression="execution(* com.*.*Service.*(..))"  
		id="mypoint"/> 
		<aop:aspect id="MyAspect" ref="logAdvice">
			<aop:around method="around"  pointcut-ref="mypoint"/>
		</aop:aspect>
	</aop:config>
 	
</beans>

```



#### (2) LoggerAdvice

함수가 실행될때마다 해당 클래스를 같이 돌게 만들어줌. XML을통해 연동해주어야한다.

```java
package com.frame;

import java.util.Date;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.Signature;

public class LoggerAdvice {
	public void beforeLog(JoinPoint jp){
		Object [] arg = jp.getArgs();
		Signature si = jp.getSignature();
		
		Date d = new Date();
		System.out.println(d.toString()+
				" Before Log:"+si.getName()+":"+
				":"+arg[0]);
	}
	public void afterLog(JoinPoint jp){
		Signature si = jp.getSignature();
		System.out.println("After Log:"+si.getName());
	}
	public void afterReturnLog(JoinPoint jp,Object returnVal){
		Signature si = jp.getSignature();
		System.out.println("afterReturnLog:"+si.getName()+":"+returnVal);
	}
	public void afterEx(JoinPoint jp, Exception exObj){
		Signature si = jp.getSignature();
		System.out.println("afterEx Log:"+si.getName());
		System.out.println("Exception:"+exObj.getMessage());
	}
	public Object around(ProceedingJoinPoint process){
		Object result = null;
		Signature si = process.getSignature();	
		String className = process.getTarget().toString(); 
		long start = System.currentTimeMillis();
		//System.out.println("Before:"+si.getName()+" "+className);
		try {
			result = process.proceed();
		} catch (Throwable e) {
			e.printStackTrace();
		}
		long end = System.currentTimeMillis();
		System.out.println(
				si.getName()+" 함수 실행 시간 "+(end-start)+"ms");
		//System.out.println("After:"+si.getName()+" "+className);
		return result;
	}
}

```

---



### 2. Anotation을 활용하여 AOP처리하기.

####  (1)XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:context="http://www.springframework.org/schema/context" 
       xmlns:aop="http://www.springframework.org/schema/aop" 
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context-3.0.xsd
       http://www.springframework.org/schema/aop 
       http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
       ">
	<context:component-scan base-package="com.*"/>
 	<aop:aspectj-autoproxy/>
 	<bean id="logAdvice" class="com.frame.LoggerAdvice"/>
 	
</beans>

```



#### (2) LoggerAdvice

```java
package com.frame;

import java.util.Date;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.Signature;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.AfterThrowing;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class LoggerAdvice {
	
	@Before("execution(* com.user.*Service.*(..))")
	public void beforeLog(JoinPoint jp){
		Object [] arg = jp.getArgs();
		Signature si = jp.getSignature();
		
		Date d = new Date();
		System.out.println(d.toString()+
				" Before Log:"+si.getName() );
	}
	@After("execution(* com.product.*Service.*(..))")
	public void afterLog(JoinPoint jp){
		Signature si = jp.getSignature();
		System.out.println("-----------After Log:"+si.getName());
	}
	@After("execution(* com.dao.UserDao.get(..))")
	public void aftergetLog(JoinPoint jp){
		Signature si = jp.getSignature();
		System.out.println("-----------After dao GET Log:"+si.getName());
	}
	@AfterReturning(pointcut="execution(* com.service.UserService.get(..))",
			        returning="returnVal")
	public void afterReturnLog(JoinPoint jp,Object returnVal){
		Signature si = jp.getSignature();
		System.out.println("----afterReturn send Mail:"+si.getName()+":"+returnVal);
	}
	@AfterThrowing(pointcut="execution(* com.service.UserService.get(..))",
	               throwing="exObj")
	public void afterEx(JoinPoint jp, Exception exObj){
		Signature si = jp.getSignature();
		System.out.println("---- afterEx Log:"+si.getName());
		System.out.println(jp.getArgs()[0]);
		System.out.println("---- Alert Admin:"+exObj.getMessage());
	}
	@Around("execution(* com.*.*Service.*(..))")
	public Object around(ProceedingJoinPoint process){
		Object result = null;
		Signature si = process.getSignature();	
		String className = process.getTarget().toString(); 
		long start = System.currentTimeMillis();
		System.out.println("***Before:"+si.getName()+" "+className);
		try {
			result = process.proceed();
		} catch (Throwable e) {
			e.printStackTrace();
		}
		long end = System.currentTimeMillis();
		System.out.println(
				si.getName()+" 함수 실행 시간 "+(end-start)+"ms");
		System.out.println("***After:"+si.getName()+" "+className);
		return result;
	}
}
```



## SQL과 연동

### Spring + Mybatis

#### 1) pom.xml에 mybatis driver setting

#### 2) spring.xml에 database 및 mybatis 관련 setting

#### 3) mybatis.xml setting



### (1) XML (SQL,mybatis setting)

sql 서버 연동, mybatis setting

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:context="http://www.springframework.org/schema/context" 
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx" 
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context 
       http://www.springframework.org/schema/context/spring-context-3.0.xsd
       http://www.springframework.org/schema/aop 
       http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
       http://www.springframework.org/schema/tx 
       http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
       ">
	<context:component-scan base-package="com.*"/>
 	<tx:annotation-driven transaction-manager="txManager"/> 
 	
 	<!-- 1. Database Setting -->
 	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
 		<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
 		<property name="url" value="jdbc:mysql://127.0.0.1:3306/shopdb?serverTimezone=Asia/Seoul"/>
 		<property name="username" value="admin1"/>
 		<property name="password" value="111111"/>
 	</bean>

 	<!-- 2. Transaction Setting -->
 	<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
 		<property name="dataSource" ref="dataSource"/>
 	</bean>
 	
 	
 	
 	<!-- 3. MyBatis Setting -->
 	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
 		<property name="dataSource" ref="dataSource"/>
 		<property name="configLocation" value="classpath:com/config/mybatis.xml"/>
 	</bean>
 	<!-- 4. Spring Mybatis Connect -->
 	<bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
 		<constructor-arg ref="sqlSessionFactory"/>
 	</bean>
 	<!-- 5. Mapper Setting -->
 	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
 		<property name="basePackage" value="com.mapper"/>
 	</bean>
 	
 	
 	
</beans>
```



### (2)mybatis.xml setting

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org/DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<typeAliases>
		<typeAlias type="com.vo.UserVO" alias="user"/>
		<typeAlias type="com.vo.ProductVO" alias="product"/>
	</typeAliases>
	
	<mappers>
		<mapper resource="com/config/usermapper.xml"/>
		<mapper resource="com/config/productmapper.xml"/>
	</mappers>
</configuration>
```



### (3) create mapper 

Dao와 동일한거임

```java
package com.mapper;

import java.util.List;

import com.vo.ProductVO;

public interface ProductMapper {
	
	public void insert(ProductVO obj);
	public void update(ProductVO obj);
	public void delete(Integer obj);
	public ProductVO select(Integer obj);
	public List<ProductVO> selectAll();
	
	
}
```



### (4) create service

interface service 생성후 개별적 생성.

```java
package com.user;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Service;
import com.mapper.ProductMapper;
import com.vo.ProductVO;

@org.springframework.stereotype.Service("pservice")
public class ProductService implements Service<Integer, ProductVO> {
	
	@Autowired //자동으로 dao에대한것을 검색해서 가져오라는 뜻.
	ProductMapper dao;
	

	@Override
	public void register(ProductVO v) {
		dao.insert(v);
	}

	@Override
	public void remove(Integer k) {
		dao.delete(k);
	}

	@Override
	public void modify(ProductVO v) {
		dao.update(v);
	}

	@Override
	public ProductVO get(Integer k) {
		
		return dao.select(k);
	}

	@Override
	public List<ProductVO> get() {
		
		return dao.selectAll();
	}

}

```



### (5) create xml mapper

sql문과 연동.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org/DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">

	
	
<mapper namespace="com.mapper.UserMapper">
	
	<select id="select" parameterType="String" resultType="user">
		SELECT * FROM CUST WHERE ID=#{obj}
	</select>
	<select id="selectAll" resultType="user">
		SELECT * FROM CUST
	</select>
	<insert id="insert" parameterType="user">
		INSERT INTO CUST VALUES (#{id},#{pwd},#{name})
	</insert>
	<update id="update" parameterType="user">
		UPDATE CUST SET PWD=#{pwd},NAME=#{name} WHERE ID=#{id}
	</update>
	<delete id="delete" parameterType="String">
		DELETE FROM CUST WHERE ID=#{obj}
	</delete>	
	
</mapper>


```

