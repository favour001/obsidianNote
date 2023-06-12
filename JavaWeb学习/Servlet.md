### Servlet简介
* Servlet就是sun公司开发动态web的一门技术
* Sun在这些API中提供一个接口叫做：Servlet 
	* 两个步骤
		1. 编写一个类，实现Servlet接口
		2. 把开发好的java类部署到web服务器中
* 把实现了Servlet接口的java程序叫做，Servlet

### HelloServlet
Servlet接口sun公司有两个默认的类：HttpServlet，GenericServlet

1. 新建一个普通Maven项目，这个空工程就是主工程
	1. ![[Pasted image 20230613002120.png]]
	2. 如果没有的话，就在Project Structure -> Facets 添加
		![[Pasted image 20230613002206.png]]
2. 关于Maven父子工程的理解
		父项目有
	```xml
	<modules>  
		<module>servlet-01</module>  
	</modules>
	```
	子项目会有
```xml
<parent>  
	<groupId>org.example</groupId>  
	<artifactId>javaWeb</artifactId>  
	<version>1.0-SNAPSHOT</version>  
</parent>
```

父项目中的java子项目可以直接使用
```xml
son extends father
```

3. Maven环境优化
	1. 修改web.xml为最新
	2. 将maven的结构搭建完整
4. 编写一个完整的servlet程序
	1. 编写一个普通类
	2. 实现Servlet接口，这里直接继承HelloServlet
```java
	public class HelloServlet extends HttpServlet {  
  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		// ServletOutputStream outputStream = resp.getOutputStream();  
		PrintWriter writer = resp.getWriter();  
		writer.print("Hello,Servlet");  
	}  
	  
	@Override  
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		doGet(req, resp);  
	}  
}
```
5. 编写Servlet的映射
	为什么需要映射：我们写德是JAVA程序，但是要通过浏览器访问，二浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的servlet，还需给他一个浏览器能够访问的路径
```xml
	<!-- 注册Servlet-->  
	<servlet>  
		<servlet-name>hello</servlet-name>  
		<servlet-class>com.lin.servlet.HelloServlet</servlet-class>  
	</servlet>  
	<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello</url-pattern>  
	</servlet-mapping>
```
6. 配置Tomcat
	注意：配置项目发布的路径就可以了
7. 启动测试
8. 成功
![[Pasted image 20230613002507.png]]