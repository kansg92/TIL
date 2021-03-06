# ๐ขday35__Spring



## Spring

### Spring, SpringBoot

์คํ๋ง๊ณผ ์คํ๋ง๋ถํธ๋ ์์ฐํ ๋ค๋ฅด๋ค. ์คํ๋ง์ ์คํ๋ง๋ถํธ์ ์ ์ ์ด๋ฉฐ ์ฌ์ฉํ๋ ค๋ฉด ๊ต์ฅํ ๋ณต์กํ๊ณ  ์ด๋ ค์ด ์ํ๋ค์ ํด์ผํ๊ธฐ ๋๋ฌธ์  ํ๋ก์ ํธํ ๋๋ ์คํ๋ง๋ถํธ๋ฅผ ์ด์ฉํด์ ์์์ ์งํํ  ์์ ์ด๋ฉฐ, ์คํ๋ง์๋ํ ๊ฐ๋๋ ์ก๊ณ  ๋์ด๊ฐ ๊ณํ์ด๋ค.

Spring์ ์๋๊ฒ์ DI,AOP์  ๊ด์ ์ ์์์ผํ๋ค. 

spring์ผ๋ก ์น์ ๊ตฌ์ฑํ๊ธฐ ์ํด์๋ Spring MVC ํน์ SpringBoot๋ฅผ ํ์ฉํด์ ๋ง๋ค ์ ๊ฐ ์๋ค.

DI,AOP,SpringMVC,SpringBoot์ด 4๊ฐ์ง ๋ฐฉ์์ด ์์ผ๋ฉฐ

DI,AOP๊ฒฝ์ฐ XML OR Anotation์ ํ์ฉํ์ฌ ํ ์ ์์ผ๋ฉฐ, XML๋ก ์ฒ๋ฆฌ์ ์์ด ๋ง์์ง๋ฉด XML์์ ๋ชจ๋ ๊ฑธ ์ปจํธ๋กคํ๊ธฐ ๋๋ฌธ์ XML์ ๊ด๋ฆฌํ๊ธฐ ์ด๋ ค์์ง ์ ๊ฐ ์๋ค.



---

## ๐กDI(Dependency Injecton) Spring

### 1.Spring XML์ ํ์ฉํ์ฌ ์ฒ๋ฆฌํ๊ธฐ(DI:Dependency Injecton)

#### (1) interface pakage(FRAME)

- ํ์ฅ์ฑ์ ์ํด ์ธํฐํ์ด์ค๋ฅผ ํ์ฉํ์ฌ frame์ ๋ง๋ค์ด๋๊ณ  ํ์. ์๋ฐ์ ํฐ ์ฅ์ ์ด๋ค! OOP!!

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

- ํญ์ ๋ชจ๋ ๊ธฐ๋ฅ์ ํ๋์ฉ TEST๋ฅผ ํตํด ๊ฒ์ฆํ๋ ์์์ด ํ์ํ๋ค.
- TEST์์์ ๊ฐ์ฅ ์ค์ํ ์์์ค ํ๋๋ก ์ ๋๋ก ๊ท์ฐฎ์ ํ์ง๋ง์. ๋์ค์ ๊ผฌ์ฌ๋ฒ๋ฆฌ๋๊ฒ์ ๋ฐฉ์งํ  ์ ์๋ค.

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

#### (5) XMLํ์ผ

XML ํ์ผํตํด์ IOC, DI๋ฅผ ๊ตฌํํ์ฌ ์ฌ์ฉํ๋ค.

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
    	<property name="dao" ref="itemdao"></property> <!-- setter ๋ฅผ ์ด์ฉํ ์ฃผ์. -->
    </bean>
    
   	<bean id="pdao" class="com.product.ProductDao"></bean>
    <bean id="pservice" class="com.product.ProductService">
  	 	<constructor-arg name="dao" ref="pdao"/> <!-- constructor ๋ฅผ ์ด์ฉํ ์ฃผ์. -->
    </bean>
       
</beans>
```



---

### 2. Anotation ์ ํ์ฉํ์ฌ Spring ๊ตฌ์ฑํ๊ธฐ (DI:Dependency Injection)



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

- @Repository๋ฅผ ์ด์ฉํด daoํ์ฑ

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

- `@service`๋ฅผ ํ์ฉํด  uservice ํ์ฑ
- `@Autowired` ๋ฅผ ํ์ฉํ์ฌ dao์๋ํ๊ฒ์ ๊ฒ์ํ์ฌ ์ด๋ฆ ์ค์ ์ ํด์ค.

```java
package com.user; 

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Dao;
import com.frame.Service;
import com.vo.UserVO;

@org.springframework.stereotype.Service("uservice")
public class UserService implements Service<String, UserVO> {
	
	@Autowired //์๋์ผ๋ก dao์๋ํ๊ฒ์ ๊ฒ์ํด์ ๊ฐ์ ธ์ค๋ผ๋ ๋ป.
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





## ๐กAOP(Aspect Orinted Programming) Spring

๋ณด์์์ผ๋ก ๋ง๋ค์ด์ง ๊ฐ๋์ผ๋ก ํจ์๊ฐ ์คํผ๋  ๋ ๋ง๋ค ๋ณด์์ฝ๋๋ฅผ ๋ชจ๋  ํด๋์ค์ ํ๋ฒ์ ์ ์ฉํ๊ธฐ์ํด ๋ง๋ค์ด์ง ๊ฐ๋์ด๋ค. ํ๋์ ํด๋์ค๋ฅผ ์ฐ๋ํ์ฌ ๋ณด์์ ์ ์ง๋ณด์๋ฅผ ํธํ๊ฒ ํด์ค๋ค.

### 1. XML์ ํ์ฉํ์ฌ AOP์ฒ๋ฆฌํ๊ธฐ.

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
		<!-- com.user ๋ฐ์์๋ ๋ชจ๋  ํจ์, ํด๋์ค์ ์ ์ฉ.  -->
		<aop:pointcut expression="execution(* com.*.*Service.*(..))"  
		id="mypoint"/> 
		<aop:aspect id="MyAspect" ref="logAdvice">
			<aop:around method="around"  pointcut-ref="mypoint"/>
		</aop:aspect>
	</aop:config>
 	
</beans>

```



#### (2) LoggerAdvice

ํจ์๊ฐ ์คํ๋ ๋๋ง๋ค ํด๋น ํด๋์ค๋ฅผ ๊ฐ์ด ๋๊ฒ ๋ง๋ค์ด์ค. XML์ํตํด ์ฐ๋ํด์ฃผ์ด์ผํ๋ค.

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
				si.getName()+" ํจ์ ์คํ ์๊ฐ "+(end-start)+"ms");
		//System.out.println("After:"+si.getName()+" "+className);
		return result;
	}
}

```

---



### 2. Anotation์ ํ์ฉํ์ฌ AOP์ฒ๋ฆฌํ๊ธฐ.

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
				si.getName()+" ํจ์ ์คํ ์๊ฐ "+(end-start)+"ms");
		System.out.println("***After:"+si.getName()+" "+className);
		return result;
	}
}
```



## SQL๊ณผ ์ฐ๋

### Spring + Mybatis

#### 1) pom.xml์ mybatis driver setting

#### 2) spring.xml์ database ๋ฐ mybatis ๊ด๋ จ setting

#### 3) mybatis.xml setting



### (1) XML (SQL,mybatis setting)

sql ์๋ฒ ์ฐ๋, mybatis setting

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

Dao์ ๋์ผํ๊ฑฐ์

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

interface service ์์ฑํ ๊ฐ๋ณ์  ์์ฑ.

```java
package com.user;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Service;
import com.mapper.ProductMapper;
import com.vo.ProductVO;

@org.springframework.stereotype.Service("pservice")
public class ProductService implements Service<Integer, ProductVO> {
	
	@Autowired //์๋์ผ๋ก dao์๋ํ๊ฒ์ ๊ฒ์ํด์ ๊ฐ์ ธ์ค๋ผ๋ ๋ป.
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

sql๋ฌธ๊ณผ ์ฐ๋.

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

