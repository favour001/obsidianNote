### 什么是JSP
Java Server Pages: Java服务器端页面，也和Servlet一样，用于动态web技术
最大的特点：
* 写JSP就像在写HTML
* 区别：
	* HTML只给用户提供静态的数据
	* JSP页面中可以嵌入JAVA代码，为用户提供动态数据

### JSP原理
思路：JSP到底怎么执行的
* 代码层面没有任何问题
* 服务器内部工作
	* tomcat中有一个work目录
	* IDEA中使用Tomcat的会在IDEA的tomcat中生产一个work目录
* JSP页面转变成了JAVA程序

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet**

JSP最终也会被转换成为一个Java类

JSP本质上就是一个Servlet

```java
//初始化
public void _jspInit() {

}
//销毁
public void _jspDestroy() {

}
//JSPService
public void _jspService(HttpServletRequest request,HttpServletResponse response) {

}
```

1. 判断请求
2. 内置一些对象
![[Pasted image 20230620212744.png]]

3. 输出页面前增加的代码
![[Pasted image 20230620212859.png]]

4. 以上的这些个对象我们可以在JSP页面中直接使用！
![[Pasted image 20230620214416.png]]


在JSP页面中：
只要是JAVA代码就会原封不动的输出；
如果是HTML代码，就会被转换为：
```java
out.write("<html>\r\n")
```
这样的格式，输出到前端！