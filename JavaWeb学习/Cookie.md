会话：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话

**有状态会话：一个同学来过教室，下次再来教师，我们会知道这个同学，曾经来过，称之为有状态会话


客户端
1.服务端给客户端一个信件,客户端下次访问服务端带上信件就可以了；cookie
2.服务器登记你来过了，下次你来的时候我来匹配你； session

### 保存会话的两种技术
cookie
* 客户端技术（响应，请求）
session
* 服务器技术，利用这个技术，可以保存用户的会话信息？我们可以把信息或者数据放在Session中

常见场景：网站登录之后，你下次不用再登录了，第二次访问直接就上去了！

### Cookie
1. 从请求中拿到cookie信息
2. 服务器响应给客户端cookie
```java
Cookie[] cookie = req.getCookies();
cookie.getName();//获取cookie中的key
cookie.getValue();//获取cookie中的value
Cookie cookie = new Cookie("lastLoginTime",System.currentTimeMillis()+"");  //创建一个新session
cookie.setMaxAge(24*60*60);  //设置cookie的有效期
resp.addCookie(cookie);响应给客户端一个cookie
```

cookie：一般会保存在本地的，用户目录下appdata；


一个网站cookie是否存在上限
* 一个Cookie只能保存一个信息
* 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie
* Cookie大小限制4kb
* 300个cookie浏览器上线

删除Cookie
* 不设置有效期，关闭浏览器，自动失效
* 设置有效期时间为0


