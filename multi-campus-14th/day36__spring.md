# π’day36__Spring



## μμΈμν© μ²λ¦¬

- μμΈμν©μ΄ μκ²Όμ μ μ¬μ©μλ , κ°λ°μλ  μ°λ¦¬λ μμμΌνλ€.
- λ°μ΄ν°λ² μ΄μ€μ μ°λμμλ μμΈμν©μ λ§λ€μ΄μΌνλ€
- λ°μ΄ν°λ² μ΄μ€μ μ°λμ λ°μ΄νλ² μ΄μ€κ° μ£½κ±°λ λ€νΈμν¬κ° λμ΄μ§λ μν©μ΄ μκΈ°κΈ°λ νλ€.



### μμΈμ²λ¦¬

```java
package com.frame;

import java.util.List;

public interface Service<K,V> {
	public void register(V v) throws Exception;
	public void remove(K k) throws Exception;
	public void modify(V v) throws Exception;
	public V get(K k) throws Exception;
	public List<V> get() throws Exception;
	
}

```

- Interfaceμμ μμΈμν©μ λ€ λκ²¨μ€λ€.

```java
package com.mapper;

import java.util.List;

import com.vo.UserVO;

public interface UserMapper {
	
	public void insert(UserVO obj) throws Exception;
	public void update(UserVO obj) throws Exception;
	public void delete(String obj) throws Exception;
	public UserVO select(String obj) throws Exception;
	public List<UserVO> selectAll() throws Exception;
	
	
}
```

- mapper(dao) λ λμΌνκ² λκ²¨μ€λ€.

```java
package com.user;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Service;
import com.mapper.UserMapper;
import com.vo.UserVO;

@org.springframework.stereotype.Service("uservice")
public class UserService implements Service<String, UserVO> {
	
	@Autowired //μλμΌλ‘ daoμλνκ²μ κ²μν΄μ κ°μ Έμ€λΌλ λ».
	UserMapper dao;

	@Override
	public void register(UserVO v) throws Exception {
		
		dao.insert(v);
	}

	@Override
	public void remove(String k) throws Exception {
		// TODO Auto-generated method stub
		dao.delete(k);
	}

	@Override
	public void modify(UserVO v) throws Exception {
		// TODO Auto-generated method stub
		dao.update(v);
	}

	@Override
	public UserVO get(String k) throws Exception {
		// TODO Auto-generated method stub
		return dao.select(k);
	}

	@Override
	public List<UserVO> get() throws Exception {
		// TODO Auto-generated method stub
		return dao.selectAll();
	}
	
	
	
}

```

- μλΉμ€μ ν¨μλ€λ λͺ¨λ λκ²¨μ€λ€.