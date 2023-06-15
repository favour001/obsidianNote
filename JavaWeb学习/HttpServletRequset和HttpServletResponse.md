web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse
* 如果要获取客户端请求过来的参数：找HttpServletRequest
* 如果要给客户端响应一些信息：找HttpServletResponse

### 简单分类
负责向浏览器发送数据的方法

```java
ServletOutputStream getOutputStream() throws IOExeption;//读取流
PrintWriter getWriter() throws IOExeption;
```

负责向浏览器发送响应头的方法
```java
public void setCharacterEncoding(String charset);  
  
/**  
* Sets the length of the content body in the response  
* In HTTP servlets, this method sets the HTTP Content-Length header.  
*  
* @param len an integer specifying the length of the  
* content being returned to the client; sets the Content-Length header  
*/  
public void setContentLength(int len);  
  
/**  
* Sets the length of the content body in the response  
* In HTTP servlets, this method sets the HTTP Content-Length header.  
*  
* @param len a long specifying the length of the  
* content being returned to the client; sets the Content-Length header  
*  
* @since Servlet 3.1  
*/  
public void setContentLengthLong(long len);  
  
/**  
* Sets the content type of the response being sent to  
* the client, if the response has not been committed yet.  
* The given content type may include a character encoding  
* specification, for example, <code>text/html;charset=UTF-8</code>.  
* The response's character encoding is only set from the given  
* content type if this method is called before <code>getWriter</code>  
* is called.  
* <p>This method may be called repeatedly to change content type and  
* character encoding.  
* This method has no effect if called after the response  
* has been committed. It does not set the response's character  
* encoding if it is called after <code>getWriter</code>  
* has been called or after the response has been committed.  
* <p>Containers must communicate the content type and the character  
* encoding used for the servlet response's writer to the client if  
* the protocol provides a way for doing so. In the case of HTTP,  
* the <code>Content-Type</code> header is used.*  
* @param type a <code>String</code> specifying the MIME* type of the content  
*  
* @see #setLocale  
* @see #setCharacterEncoding  
* @see #getOutputStream  
* @see #getWriter  
*  
*/  
  
public void setContentType(String type);
public void setDateHeader(String name, long date);  
  
/**  
*  
* Adds a response header with the given name and  
* date-value. The date is specified in terms of  
* milliseconds since the epoch. This method allows response headers  
* to have multiple values.  
*  
* @param name the name of the header to set  
* @param date the additional date value  
*  
* @see #setDateHeader  
*/  
public void addDateHeader(String name, long date);  
  
/**  
*  
* Sets a response header with the given name and value.  
* If the header had already been set, the new value overwrites the  
* previous one. The <code>containsHeader</code> method can be* used to test for the presence of a header before setting its  
* value.  
*  
* @param name the name of the header  
* @param value the header value If it contains octet string,  
* it should be encoded according to RFC 2047  
* (http://www.ietf.org/rfc/rfc2047.txt)  
*  
* @see #containsHeader  
* @see #addHeader  
*/  
public void setHeader(String name, String value);  
  
/**  
* Adds a response header with the given name and value.  
* This method allows response headers to have multiple values.  
*  
* @param name the name of the header  
* @param value the additional header value If it contains  
* octet string, it should be encoded  
* according to RFC 2047  
* (http://www.ietf.org/rfc/rfc2047.txt)  
*  
* @see #setHeader  
*/  
public void addHeader(String name, String value);  
  
/**  
* Sets a response header with the given name and  
* integer value. If the header had already been set, the new value  
* overwrites the previous one. The <code>containsHeader</code>  
* method can be used to test for the presence of a header before  
* setting its value.  
*  
* @param name the name of the header  
* @param value the assigned integer value  
*  
* @see #containsHeader  
* @see #addIntHeader  
*/  
public void setIntHeader(String name, int value);  
  
/**  
* Adds a response header with the given name and  
* integer value. This method allows response headers to have multiple  
* values.  
*  
* @param name the name of the header  
* @param value the assigned integer value  
*  
* @see #setIntHeader  
*/  
public void addIntHeader(String name, int value);
```

响应的状态码
```java
/**  
* Status code (100) indicating the client can continue.  
*/  
public static final int SC_CONTINUE = 100;  
  
/**  
* Status code (101) indicating the server is switching protocols  
* according to Upgrade header.  
*/  
public static final int SC_SWITCHING_PROTOCOLS = 101;  
  
/**  
* Status code (200) indicating the request succeeded normally.  
*/  
public static final int SC_OK = 200;  
  
/**  
* Status code (201) indicating the request succeeded and created  
* a new resource on the server.  
*/  
public static final int SC_CREATED = 201;  
  
/**  
* Status code (202) indicating that a request was accepted for  
* processing, but was not completed.  
*/  
public static final int SC_ACCEPTED = 202;  
  
/**  
* Status code (203) indicating that the meta information presented  
* by the client did not originate from the server.  
*/  
public static final int SC_NON_AUTHORITATIVE_INFORMATION = 203;  
  
/**  
* Status code (204) indicating that the request succeeded but that  
* there was no new information to return.  
*/  
public static final int SC_NO_CONTENT = 204;  
  
/**  
* Status code (205) indicating that the agent <em>SHOULD</em> reset* the document view which caused the request to be sent.  
*/  
public static final int SC_RESET_CONTENT = 205;  
  
/**  
* Status code (206) indicating that the server has fulfilled  
* the partial GET request for the resource.  
*/  
public static final int SC_PARTIAL_CONTENT = 206;  
  
/**  
* Status code (300) indicating that the requested resource  
* corresponds to any one of a set of representations, each with  
* its own specific location.  
*/  
public static final int SC_MULTIPLE_CHOICES = 300;  
  
/**  
* Status code (301) indicating that the resource has permanently  
* moved to a new location, and that future references should use a  
* new URI with their requests.  
*/  
public static final int SC_MOVED_PERMANENTLY = 301;  
  
/**  
* Status code (302) indicating that the resource has temporarily  
* moved to another location, but that future references should  
* still use the original URI to access the resource.  
*  
* This definition is being retained for backwards compatibility.  
* SC_FOUND is now the preferred definition.  
*/  
public static final int SC_MOVED_TEMPORARILY = 302;  
  
/**  
* Status code (302) indicating that the resource reside  
* temporarily under a different URI. Since the redirection might  
* be altered on occasion, the client should continue to use the  
* Request-URI for future requests.(HTTP/1.1) To represent the  
* status code (302), it is recommended to use this variable.  
*/  
public static final int SC_FOUND = 302;  
  
/**  
* Status code (303) indicating that the response to the request  
* can be found under a different URI.  
*/  
public static final int SC_SEE_OTHER = 303;  
  
/**  
* Status code (304) indicating that a conditional GET operation  
* found that the resource was available and not modified.  
*/  
public static final int SC_NOT_MODIFIED = 304;  
  
/**  
* Status code (305) indicating that the requested resource  
* <em>MUST</em> be accessed through the proxy given by the* <code><em>Location</em></code> field.*/  
public static final int SC_USE_PROXY = 305;  
  
/**  
* Status code (307) indicating that the requested resource  
* resides temporarily under a different URI. The temporary URI  
* <em>SHOULD</em> be given by the <code><em>Location</em></code>  
* field in the response.  
*/  
public static final int SC_TEMPORARY_REDIRECT = 307;  
  
/**  
* Status code (400) indicating the request sent by the client was  
* syntactically incorrect.  
*/  
public static final int SC_BAD_REQUEST = 400;  
  
/**  
* Status code (401) indicating that the request requires HTTP  
* authentication.  
*/  
public static final int SC_UNAUTHORIZED = 401;  
  
/**  
* Status code (402) reserved for future use.  
*/  
public static final int SC_PAYMENT_REQUIRED = 402;  
  
/**  
* Status code (403) indicating the server understood the request  
* but refused to fulfill it.  
*/  
public static final int SC_FORBIDDEN = 403;  
  
/**  
* Status code (404) indicating that the requested resource is not  
* available.  
*/  
public static final int SC_NOT_FOUND = 404;  
  
/**  
* Status code (405) indicating that the method specified in the  
* <code><em>Request-Line</em></code> is not allowed for the resource* identified by the <code><em>Request-URI</em></code>.  
*/  
public static final int SC_METHOD_NOT_ALLOWED = 405;  
  
/**  
* Status code (406) indicating that the resource identified by the  
* request is only capable of generating response entities which have  
* content characteristics not acceptable according to the accept  
* headers sent in the request.  
*/  
public static final int SC_NOT_ACCEPTABLE = 406;  
  
/**  
* Status code (407) indicating that the client <em>MUST</em> first* authenticate itself with the proxy.  
*/  
public static final int SC_PROXY_AUTHENTICATION_REQUIRED = 407;  
  
/**  
* Status code (408) indicating that the client did not produce a  
* request within the time that the server was prepared to wait.  
*/  
public static final int SC_REQUEST_TIMEOUT = 408;  
  
/**  
* Status code (409) indicating that the request could not be  
* completed due to a conflict with the current state of the  
* resource.  
*/  
public static final int SC_CONFLICT = 409;  
  
/**  
* Status code (410) indicating that the resource is no longer  
* available at the server and no forwarding address is known.  
* This condition <em>SHOULD</em> be considered permanent.*/  
public static final int SC_GONE = 410;  
  
/**  
* Status code (411) indicating that the request cannot be handled  
* without a defined <code><em>Content-Length</em></code>.  
*/  
public static final int SC_LENGTH_REQUIRED = 411;  
  
/**  
* Status code (412) indicating that the precondition given in one  
* or more of the request-header fields evaluated to false when it  
* was tested on the server.  
*/  
public static final int SC_PRECONDITION_FAILED = 412;  
  
/**  
* Status code (413) indicating that the server is refusing to process  
* the request because the request entity is larger than the server is  
* willing or able to process.  
*/  
public static final int SC_REQUEST_ENTITY_TOO_LARGE = 413;  
  
/**  
* Status code (414) indicating that the server is refusing to service  
* the request because the <code><em>Request-URI</em></code> is longer* than the server is willing to interpret.  
*/  
public static final int SC_REQUEST_URI_TOO_LONG = 414;  
  
/**  
* Status code (415) indicating that the server is refusing to service  
* the request because the entity of the request is in a format not  
* supported by the requested resource for the requested method.  
*/  
public static final int SC_UNSUPPORTED_MEDIA_TYPE = 415;  
  
/**  
* Status code (416) indicating that the server cannot serve the  
* requested byte range.  
*/  
public static final int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;  
  
/**  
* Status code (417) indicating that the server could not meet the  
* expectation given in the Expect request header.  
*/  
public static final int SC_EXPECTATION_FAILED = 417;  
  
/**  
* Status code (500) indicating an error inside the HTTP server  
* which prevented it from fulfilling the request.  
*/  
public static final int SC_INTERNAL_SERVER_ERROR = 500;  
  
/**  
* Status code (501) indicating the HTTP server does not support  
* the functionality needed to fulfill the request.  
*/  
public static final int SC_NOT_IMPLEMENTED = 501;  
  
/**  
* Status code (502) indicating that the HTTP server received an  
* invalid response from a server it consulted when acting as a  
* proxy or gateway.  
*/  
public static final int SC_BAD_GATEWAY = 502;  
  
/**  
* Status code (503) indicating that the HTTP server is  
* temporarily overloaded, and unable to handle the request.  
*/  
public static final int SC_SERVICE_UNAVAILABLE = 503;  
  
/**  
* Status code (504) indicating that the server did not receive  
* a timely response from the upstream server while acting as  
* a gateway or proxy.  
*/  
public static final int SC_GATEWAY_TIMEOUT = 504;  
  
/**  
* Status code (505) indicating that the server does not support  
* or refuses to support the HTTP protocol version that was used  
* in the request message.  
*/  
public static final int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

### 常见应用
1. 向浏览器输出消息
2. 下载文件
	1. 要获取下载文件的路径
	2. 下载的文件名是啥
	3. 设置想办法让浏览器能够支持（Content-Disposition）下载我们需要的东西，中文文件名URLEncoder.encode编码，否则有可能乱码
	4. 获取下载文件的输入流
	5. 创建缓冲区
	6. 获取outputStream对象
	7. 将FileOutputStream流写入到buffer缓冲区
	8. 使用OutputStream将缓冲区中的数据输出到客户端
```java
public class FileServlet extends HttpServlet {  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	String realPath = "D:\\JavaWeb-Study\\response\\src\\main\\resources\\background.jpg";  
	  
	// String realPath = this.getServletContext().getRealPath(rPath);  
	System.out.println("下载文件的路径："+realPath);  
	String fileName = realPath.substring(realPath.lastIndexOf("\\")+1);  
	resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(fileName,"utf-8"));  
	  
	FileInputStream in = new FileInputStream(realPath);  
	  
	int len = 0;  
	byte[] buffer = new byte[1024];  
	  
	ServletOutputStream out = resp.getOutputStream();  
	while ((len=in.read(buffer))>0){  
	out.write(buffer,0,len);  
	}  
	in.close();  
	out.close();  
}  
}
```

3. 验证码
```java
public class ImageServlet extends HttpServlet {  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	//如何让浏览器5秒自动刷新一次  
	resp.setHeader("refresh","3");  
	  
	//在内存中创建一个图片  
	BufferedImage bufferedImage = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);  
	//得到图片  
	Graphics2D graphics2D = (Graphics2D) bufferedImage.getGraphics();//一支笔  
	//设置图片的背景颜色  
	graphics2D.setColor(Color.white);  
	graphics2D.fillRect(0,0,80,20);  
	//给图片写数据  
	graphics2D.setColor(Color.blue);  
	graphics2D.setFont(new Font(null,Font.BOLD,20));  
	graphics2D.drawString(makeNum(),0,20);  
	  
	//告诉浏览器，这个请求用图片的方式打开  
	resp.setContentType("image/png");  
	  
	resp.setDateHeader("expires",-1);  
	resp.setHeader("Cache-Control","no-cache");  
	resp.setHeader("Pragma","no-cache");  
	  
	//把图片写给浏览器  
	  
	ImageIO.write(bufferedImage,"jpg",resp.getOutputStream());  
}  
  
public String makeNum(){  
	Random random = new Random();  
	String num = random.nextInt(9999)+"";  
	StringBuffer stringBuffer = new StringBuffer();  
	for (int i = 0; i < 4-num.length(); i++) {  
		stringBuffer.append("0");  
	}  
	String s = stringBuffer.toString() + num;  
	return num;  
}
```

4. 重定向
一个web资源收到客户端请求后，他会通知客户端去访问另外一个web资源，这个过程叫重定向
常见场景
* 用户登录
```java
public class RedirectServlet extends HttpServlet {  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		//重定向  
		resp.setHeader("Location","/r/img");  
		resp.sendRedirect("/r/img");  
		resp.setStatus(302);  
	  
	}  
	  
	@Override  
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		doGet(req,resp);  
	}  
}
```
面试题: 请你聊聊重定向和转发的区别？
相同点：
* 页面都会实现跳转
不同点：
* 请求转发的时候，url不会产生变化 307
* 重定向时候，url地址栏会发生变化 302


```java
public class RequestTest extends HttpServlet {  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		String username = req.getParameter("username");  
		String password = req.getParameter("password");  
		System.out.println(username+":"+password);  
		// 重定向时候一定要注意，路径问题，否则404  
		resp.sendRedirect("/r/success/jsp");  
	}  
	  
	@Override  
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		doGet(req, resp);  
	}  
}
```

### HttpServletRequest
HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有信息


获取前端传递的参数

```java
public class LoginServlet extends HttpServlet {  
	@Override  
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
	  
		req.setCharacterEncoding("utf-8");  
		resp.setCharacterEncoding("utf-8");  
		  
		String username = req.getParameter("username");  
		String password = req.getParameter("password");  
		String[] hobbys = req.getParameterValues("hobbys");  
		//后台接收中文乱码问题  
		System.out.println(username);  
		System.out.println(password);  
		System.out.println(Arrays.toString(hobbys));  
		//这里的/代表当前web应用  
		req.getRequestDispatcher(req.getContextPath()+"/success.jsp").forward(req,resp);  
	}  
	  
	@Override  
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {  
		doGet(req, resp);  
	}  
}
```