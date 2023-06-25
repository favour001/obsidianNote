**jsp表达式**
```jsp
<%--  
jsp表达式  
作用：用来将程序的输出，输出到客户端  
<%=变量或者表达式%>  
--%>  
<%= new java.util.Date()%>
```

jsp代码
```jsp
	<%  
		int sum = 0;  
		for (int i = 0; i < 100; i++) {  
			sum += i;  
		}  
		out.println("<h1>Sum="+sum+"</h1>");  
	%>  
	  
	<%--在代码嵌入HTML元素--%>  
	<%  
		for (int i = 0; i < 5; i++) {  
	%>  
		<h1>hello,world <%=i%> </h1>  
	<%  
		}  
	%>
	<%--EL表达式--%>  
	<% for (int i = 0; i < 5; i++) {  %>  
		<h1>hello,world ${i} </h1>  
	<%  }  %>
```


JSP声明
```jsp
<%!  
static {  
	System.out.println("Loading Servlet");  
	}  
	private int globalVar = 0;  
	  
	public void test(){  
	System.out.println("进去了");  
}  
%>
```
JSP声明：会被编译到JSP生成JAVA的类中！其他的，就会被生成到_jspService方法中

在JSP，嵌入JAVA代码即可！
```jsp
<%%>
<%=%>
<%!%>
<%----%>
```

JSP的注释，不会在客户端显示，HTML就会

```jsp
<%--@include会将两个页面合二为一--%>
<%@ page arg... %>
<%@include arg... %>
<%--JSP标签
jsp:include:拼接页面，本质还是三个
--%>
<jsp:include page=""/>
```

### 九大内置对象
* PageContext 存东西
* Request 存东西
* Response
* Session 存东西
* Application 【PageContext】存东西
* config【servletConfig】
* out
* page
* excepetion

```jsp
<body>  
<%  
	pageContext.setAttribute("name1","噫噫噫1");//保存的数据只在一个页面中有效  
	request.setAttribute("name2","噫噫噫2");//保存的数据只在一次请求中有效，请求转发会携带这个数据  
	session.setAttribute("name3","噫噫噫3");//保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器  
	application.setAttribute("name4","噫噫噫4");//保存的数据只在服务器中有效，从打开服务器到关闭服务器  
%>  
  
<%--脚本片段中的代码，会被原封不动生成到JSP.java  
要求：这里面的代码，必须保证Java语法的正确性  
--%>  
  
<%  
	//从pageContext取出，我们通过寻找的方式来  
	String name1 = (String) pageContext.findAttribute("name1");  
	String name2 = (String) pageContext.findAttribute("name2");  
	String name3 = (String) pageContext.findAttribute("name3");  
	String name4 = (String) pageContext.findAttribute("name4");  
	String name5 = (String) pageContext.findAttribute("name5");  
%>  
  
	<%--使用EL表达式输出 ${}--%><h1>取出结果为：</h1>  
	<h3>${name1}</h3>  
	<h3>${name2}</h3>  
	<h3>${name3}</h3>  
	<h3>${name4}</h3>  
	<h3>${name5}</h3>  
	<h3><%=name5%></h3>  
</body>
```

作用域
```java
public static final int PAGE_SCOPE = 1;
public static final int REQUEST_SCOPE = 2;
public static final int SESSION_SCOPE = 3;
public static final int APPLICATION_SCOPE = 4;
```

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如：新闻
session：客户端向服务器发送请求，产生的数据，用户用完一会还有用，比如：购物车；
application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据

### JSP标签、JSTL标签、EL表达式
EL表达式
* 获取数据
* 执行运算
* 获取web开发的常用对象
* 调用Java对象

JSP标签
```jsp
<%--转到另一个页面--%>  
<jsp:forward page="/pageConetxtDemo3.jsp">  
<%-- 通过标签携带参数--%>  
<jsp:param name="name" value="xxx"/>  
<jsp:param name="age" value="12"/>  
</jsp:forward>
```

JSTL表达式
* 引入对应的taglib
* 使用其中的放啊
* 在Tomcat也需要引入jstl的包，否则会报错，JSTL解析错误


```jsp
<form action="coreif.jsp" method="get">  
<%--  
EL表达式获取表单中的数据  
${param.参数名}  
--%>  
<input type="text" name="username" value="${param.username}">  
<input type="submit" value="登录">  
</form>  
  
<c:if test="${param.username == 'admin'}" var="isAdmin">  
<c:out value="管理员欢迎您"/>  
</c:if>  
  
<c:out value="${isAdmin}"/>  
  
  
  
  
<%--定义一个变量score，值为85--%>  
<c:set var="score" value="85"/>  
<c:choose>  
<c:when test="${score>=90}">  
你的成绩为优秀  
</c:when>  
<c:when test="${score>=80}">  
你的成绩为良好  
</c:when>  
<c:when test="${score>=70}">  
你的成绩为优秀  
</c:when>  
<c:when test="${score>=60}">  
你的成绩为优秀  
</c:when>  
</c:choose>  
  
<%  
ArrayList<String> people = new ArrayList<>();  
people.add(0,"zz");  
people.add(1,"zz");  
people.add(2,"zz");  
people.add(3,"zz");  
people.add(4,"zz");  
request.setAttribute("list",people);  
%>  
<%--  
var,每一次遍历出来的变量  
items,要遍历的对象  
begin, 哪里开始  
end, 到哪里  
step 步长  
--%>  
<c:forEach var="people" items="${list}">  
<c:out value="${people}"/>  
</c:forEach>  
  
<c:forEach var="people" items="${list}" begin="1" end="3" step="2">  
<c:out value="${people}"/>  
</c:forEach>
```