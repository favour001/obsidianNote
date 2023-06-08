### 抽取公共方法
```java
package com.lin.utils;import org.apache.ibatis.io.Resources;import org.apache.ibatis.session.SqlSession;import org.apache.ibatis.session.SqlSessionFactory;import org.apache.ibatis.session.SqlSessionFactoryBuilder;import java.io.IOException;import java.io.InputStream;

//sqlSessionFactory --> sqlSessionpublic 
class MybatisUtils {    
    private static SqlSessionFactory sqlSessionFactory;    
    static{        
        try{            
        //使用mybatis第一步：获取sqlSessionFactory对象            
            String resource = "mybatis-config.xml";            
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);        
        } catch (IOException e){            
            e.printStackTrace();        
        }   
    }    
//既然又了SqlSessionFactory，顾名思义，我们就可以从中获取SqlSession的实例了。    //SqlSession 完全包含了面向数据库执行SQL命令所需的所有方法    
    public static SqlSession getSqlSession(){        
        return sqlSessionFactory.openSession();    
    }
}
```

### 编写mybatis-config.xml
```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE configuration         
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"        
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>    
    <environments default="development">        
        <environment id="development">            
            <transactionManager type="JDBC"/>            
            <dataSource type="POOLED">                
            <property name="driver" value="com.mysql.cj.jdbc.Driver"/>                
            <property name="url" value="jdbc:mysql://127.0.0.1:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
            <property name="username" value="root"/>                
            <property name="password" value="root"/>            
            </dataSource>        
        </environment>    
    </environments>
    <!--    每一个Mapper.xml都需要在Mybatis核心配置文件中注册！-->
    <mappers>        
        <mapper resource="com/lin/dao/UserMapper.xml"/>    
    </mappers>
</configuration>
```

### 编写JavaBean实体类
#### POJO
对应数据库里的某一张表，pojo里的每一个属性都和该表中的字段一一对应
```java
public class Uesr{
    private int id;
    private String name;
    private String pwd
}
```
![e043b5fd8890dc922224afff2062b08d.png](en-resource://database/650:1)

### 接口类和mapper.xml
#### DAO定义了在一个模型对象上要执行的标准操作
```java
public interface UserDap{
    List<User> getUserList();
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper        
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"        
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.lin.dao.UserDao">
    <!--    查询语句-->  
    <select id="getUserList" resultType="com.lin.pojo.User">      
        select * from mybatis.user  
    </select>
</mapper>
```


### 测试类
```java
package com.lin.dao;
import com.lin.pojo.User;
import com.lin.utils.MybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;
import java.util.List;
public class UserDaoTest {    
    @Test    
    public void test(){        
        //第一步：获得SqlSession对象        
        SqlSession sqlSession = MybatisUtils.getSqlSession();        
        //方式一；getMapper        
        UserDao userDao = sqlSession.getMapper(UserDao.class);        
        List<User> userList = userDao.getUserList();       
        //方式二：        
        //不推荐使用    
        //List<User> userList = sqlSession.selectList("com.lin.dao.getUserList");        
        for (User user : userList){            
        System.out.println(user);        
        }        
        sqlSession.close();   
    }
}
```



### 遇到的错误
注意点
org.apache.ibatis.binding.BindingException: Type interface com.lin.dao.UserDao is not known to the MapperRegistry.
###### MapperRegistry
maven由于它的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题，
pom
```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
<build>    
    <resources>        
        <resource>            
            <directory>src/main/resources</directory>
            <includes>                
                <include>**/*.properties</include>                
                <include>**/*.xml</include>            
            </includes>            
            <filtering>true</filtering>        
        </resource>        
        <resource>            
            <directory>src/main/java</directory>            
            <includes>                
                <include>**/*.properties</include>                
                <include>**/*.xml</include>            
            </includes>            
            <filtering>true</filtering>        
        </resource>    
    </resources>
</build>
```