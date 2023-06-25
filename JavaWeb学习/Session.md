什么是Session：
* 服务器会给每一个用户（浏览器）创建一个Session对象
* 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
* 用户登录之后，整个网站它都可以访问 -->保存用户的信息；保存购物车的信息


Session和Cookie的区别：
* Cookie是把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）
* Session把用户的数据写到用户独占Session中，服务器端保存（保存重要的信息，减少服务器资源的浪费）
* Session对象由服务器创建；

使用场景：
* 保存一个登录用户的信息；
* 购物车信息
* 在整个网站中经常会使用的数据，我们将它保存在Session中

使用Session:
```java
public class SessionDemo extends HttpServlet {  
@Override  
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	//解决乱码问题  
	resp.setCharacterEncoding("utf-8");  
	req.setCharacterEncoding("utf-8");  
	resp.setContentType("text/html;charset=utf-8");  
	  
	// 得到Session  
	HttpSession session = req.getSession();  
	  
	// 给Session中存东西  
	session.setAttribute("name",new Person("小样",12));  
	  
	// 获取Session的id  
	String id = session.getId();  
	  
	  
	// 判断Session是不是新创建的  
	if (session.isNew()){  
	resp.getWriter().write("session创建成功,ID"+id);  
	}else {  
	resp.getWriter().write("已经创建了");  
	}  
	  
	Cookie cookie = new Cookie("JSESSIONID",id);  
	  
	resp.addCookie(cookie);  
  
  
}  
  
@Override  
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	doGet(req, resp);  
}  
}
```


```java
public class SessionDemo1 extends HttpServlet {  
@Override  
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	//解决乱码问题  
	resp.setCharacterEncoding("utf-8");  
	req.setCharacterEncoding("utf-8");  
	resp.setContentType("text/html;charset=utf-8");  
	  
	// 得到Session  
	HttpSession session = req.getSession();  
	  
	Person person = (Person) session.getAttribute("name");  
	  
	System.out.println(person.toString());  
}  
  
@Override  
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	doGet(req, resp);  
}  
}
```


session过期
```java
public class SessionDemo2 extends HttpServlet {  
@Override  
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	//注销  
	HttpSession session = req.getSession();  
	  
	session.removeAttribute("name");  
	// 手动注销  
	session.invalidate();  
}  
  
@Override  
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	doGet(req, resp);  
}  
}
```

xml配置会话过期
```xml
<!-- 设置Session默认的失效时间-->  
<session-config>  
<!-- 15分钟后Session自动失效，以分钟为单位-->  
	<session-timeout>1</session-timeout>  
</session-config>
```

![[Pasted image 20230619232557.png]]