Model
view
Controller



![[Pasted image 20230624224445.png]]

servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护
servlet的代码，处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码

程序员
|
JDBC
|
Mysql Orcal  SqlServer


![[Pasted image 20230624225419.png]]

Model
* 业务处理：业务逻辑（Service）
* 数据持久层：CRUD（Dao）
View
* 展示数据
* 提供连接发起Servlet请求（a,form,img）
Controller（Servlet）
* 接收用户的请求：（req：请求参数，Session信息）
* 交给业务层处理对应的代码
* 控制视图跳转
```java
登录-->接收用户的登录请求--->处理用户的请求(获取用户登录的参数，username，password)--->交给业务层处理登录业务（判断用户名密码是否正确：事务）--->Dao层查询用户名和密码是否正确
```