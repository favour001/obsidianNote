# 方式一

1. 编写数据源配置
2. sqlSessionFactory
3. sqlSessionTemplate
4. 需要给接口加实现类
5. 写得实现类，注入到spring配置中
6. 测试

# 方式二

```java
public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper{  
	@Override  
	public List<User> getUserLike(String value) {  
	return null;  
	}  
	  
	@Override  
	public List<User> getUserList() {  
	SqlSession sqlSession = getSqlSession();  
	UserMapper mapper = sqlSession.getMapper(UserMapper.class);  
	return mapper.getUserList();  
	}
}
```

```xml
<bean id="userMapper2" class="com.lin.dao.UserMapperImpl2">  
	<property name="sqlSessionFactory" ref="sqlSessionFactory"/>  
</bean>
```