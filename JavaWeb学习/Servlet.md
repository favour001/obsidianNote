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

### Servlet原理
Servlet是由web服务器调用，web请求
![[Pasted image 20230613213029.png]]

### Mapping

1. 一个Servlet可以指定一个映射路径
	```xml
	<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello</url-pattern>  
	</servlet-mapping>
```
2. 一个Servlet可以指定多个映射路径
	```xml
	<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello</url-pattern>  
		</servlet-mapping>  
		<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello1</url-pattern>  
		</servlet-mapping>  
		<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello2</url-pattern>  
		</servlet-mapping>  
		<servlet-mapping>  
		<servlet-name>hello</servlet-name>  
		<url-pattern>/hello3</url-pattern>  
	</servlet-mapping>
```
3. 一个Servlet可以指定通用映射路径
```xml
<servlet-mapping>  
	<servlet-name>hello</servlet-name>  
	<url-pattern>/hello/*</url-pattern>  
</servlet-mapping>
```
4. 默认请求路径
```xml
<servlet-mapping>  
	<servlet-name>hello</servlet-name>  
	<url-pattern>/*</url-pattern>  
</servlet-mapping>
```
5. 指定一些后缀或者前缀
```xml
<servlet-mapping>  
	<servlet-name>hello</servlet-name>  
	<url-pattern>*.xxx</url-pattern>  
</servlet-mapping>
```
6. 优先级问题
	指定了固有的映射路径，优先级最高，如果找不到就会走默认的处理请求
	```xml
<servlet>  
	<servlet-name>error</servlet-name>  
	<servlet-class>com.lin.servlet.ErrorServlet</servlet-class>  
</servlet>  
<servlet-mapping>  
	<servlet-name>error</servlet-name>  
	<url-pattern>/*</url-pattern>  
</servlet-mapping>
```


```java
// this.getInitParameter(); 初始化参数  
// this.getServletConfig(); Servlet配置  
// this.getServletContext(); Servlet上下文
```

### ServletContext
web容器在启动的时候，它会为每个web程序都常见一个对应的ServletContext对象，它代表了当前的web应用
* 共享数据
	在Servlet保存的数据，在另一个Servlet中获取数据
	创建一个存储数据的类
	```java
	public class HelloServlet extends HttpServlet {  
		@Override  
		protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		// this.getInitParameter(); 初始化参数  
		// this.getServletConfig(); Servlet配置  
		// this.getServletContext(); Servlet上下文  
			ServletContext servletContext = this.getServletContext();  
			  
			String username = "XX";  
			// 将一个数据保存在ServletContext中，名为username，值为username  
			servletContext.setAttribute("username",username);  
		  
		}  
}
```