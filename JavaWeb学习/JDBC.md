什么是JDBC：Java连接数据库
```java
public static void main(String[] args) throws ClassNotFoundException, SQLException {  
String url = "jdbc:mysql://127.0.0.1:3306/jdbc?useUnicode=true&characterEncoding=utf-8";  
String username = "root";  
String password = "root";  
  
//1.加载驱动  
Class.forName("com.mysql.jdbc.Driver");  
//2.连接数据库  
Connection connection = DriverManager.getConnection(url,username,password);  
//3.向数据库发送SQL的对象Statement：CRUD  
Statement statement = connection.createStatement();  
//4.编写SQL  
String sql = "select * from users;";  
  
//受影响的行数，增删改都是用executeUpdate即可  
//ResultSet resultSet = statement.executeUpdate(sql);  
  
//5.执行SQL  
ResultSet resultSet = statement.executeQuery(sql);  
while (resultSet.next()){  
  
}  
//6.关闭连接，释放资源  
resultSet.close();  
statement.close();  
connection.close();  
}
```


### 预编译

```java
public static void main(String[] args) throws ClassNotFoundException, SQLException {  
String url = "jdbc:mysql://127.0.0.1:3306/jdbc?useUnicode=true&characterEncoding=utf-8";  
String username = "root";  
String password = "root";  
  
//1.加载驱动  
Class.forName("com.mysql.jdbc.Driver");  
//2.连接数据库  
Connection connection = DriverManager.getConnection(url,username,password);  
  
//3.编写SQL  
// String sql = "select * from users;";  
  
String sql = "insert into users(id,name,password,email,birthday) values (?,?,?,?,?);";  
  
//4.预编译  
PreparedStatement preparedStatement = connection.prepareStatement(sql);  
  
preparedStatement.setInt(1,1); //给第一个占位符？的值赋值为1  
  
int i = preparedStatement.executeUpdate();  
  
if (i > 0){  
System.out.println("插入成功");  
}  
  
preparedStatement.close();  
connection.close();  
}
```

JDBC事务
ACID原则：保证数据的安全
```
开始事务
事务提交 commit()
事务回滚 rollback()
关闭事务

转账：
A(900) ----> B(1100)
```


Junit单元测试
```xml
<dependency>  
	<groupId>junit</groupId>  
	<artifactId>junit</artifactId>  
	<version>4.13.2</version>  
	<scope>compile</scope>  
</dependency>
```

简单使用
@Test注解只有再方法上有效，只要加了这个注解的方法，就可以直接运行

```java
@Test  
public void test(){  
	System.out.println("Hello");  
}
```