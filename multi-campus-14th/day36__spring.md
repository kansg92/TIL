# 📢day36__Spring



## 예외상황 처리

- 예외상황이 생겼을 시 사용자든, 개발자든 우리는 알아야한다.
- 데이터베이스와 연동시에는 예외상황을 만들어야한다
- 데이터베이스와 연동시 데이텁베이스가 죽거나 네트워크가 끊어지는 상황이 생기기도 한다.



### 예외처리

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

- Interface에서 예외상황시 다 넘겨준다.

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

- mapper(dao) 도 동일하게 넘겨준다.

```java
package com.user;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;

import com.frame.Service;
import com.mapper.UserMapper;
import com.vo.UserVO;

@org.springframework.stereotype.Service("uservice")
public class UserService implements Service<String, UserVO> {
	
	@Autowired //자동으로 dao에대한것을 검색해서 가져오라는 뜻.
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

- 서비스의 함수들도 모두 넘겨준다.