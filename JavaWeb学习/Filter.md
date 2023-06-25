filter:过滤器，用来过滤网站的数据
* 处理中文乱码
* 登录验证
![[Pasted image 20230625212305.png]]

开发步骤
1. 导包
2. 编写过滤器

```xml
<dependencies>  
<dependency>  
<groupId>javax.servlet</groupId>  
<artifactId>servlet-api</artifactId>  
<version>2.5</version>  
</dependency>  
<dependency>  
<groupId>javax.servlet.jsp</groupId>  
<artifactId>javax.servlet.jsp-api</artifactId>  
<version>2.3.3</version>  
</dependency>  
<dependency>  
<groupId>javax.servlet.jsp.jstl</groupId>  
<artifactId>jstl-api</artifactId>  
<version>1.2</version>  
</dependency>  
<dependency>  
<groupId>taglibs</groupId>  
<artifactId>standard</artifactId>  
<version>1.1.2</version>  
</dependency>  
<dependency>  
<groupId>mysql</groupId>  
<artifactId>mysql-connector-java</artifactId>  
<version>8.0.28</version>  
</dependency>  
</dependencies>
```

```java
public class CharacterEncodingFilter implements Filter {  
//初始化：web服务器启动，就已经初始化了，随时等待过滤对象出现  
@Override  
public void init(FilterConfig filterConfig) throws ServletException {  
System.out.println("初始化");  
}  
//chain:链  
/*  
1.过滤所有代码，在过滤特定请求的时候都会执行  
2.必须要让过滤器继续同行  
filterChain.doFilter(servletRequest,servletResponse)  
*/  
@Override  
public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {  
servletRequest.setCharacterEncoding("utf-8");  
servletResponse.setCharacterEncoding("utf-8");  
servletResponse.setContentType("text/html;charset=UTF-8");  
System.out.println("执行前");  
// 让我们的请求继续走，如果不写，程序到这里就被拦截停止  
filterChain.doFilter(servletRequest,servletResponse);  
}  
// 销毁：web服务器关闭的时候，过滤会销毁  
@Override  
public void destroy() {  
System.out.println("销毁");  
}  
}
```

```jsp
<servlet>  
<servlet-name>ShowServlet</servlet-name>  
<servlet-class>com.test.servlet.ShowServlet</servlet-class>  
</servlet>  
<servlet-mapping>  
<servlet-name>ShowServlet</servlet-name>  
<url-pattern>/servlet/show</url-pattern>  
</servlet-mapping>  
  
<filter>  
<filter-name>CharacterEncodingFilter</filter-name>  
<filter-class>com.test.filter.CharacterEncodingFilter</filter-class>  
</filter>  
<filter-mapping>  
<filter-name>CharacterEncodingFilter</filter-name>  
<!-- 只要是/servlet的任何请求，会经过这个过滤器-->  
<url-pattern>/servlet/*</url-pattern>  
</filter-mapping>  
</web-app>
```
