HTTP(超文本传输协议)
* 文本：html，字符串
* 超文本：图片，音乐，视频，定位，地图
* 80
HTTPS：安全的
* 443

4.2、两个时代
* http1.0
	* HTTP/1.0:客户端可以与web服务器连接，只能获得一个web资源，断开连接
* http2.0
	* HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源

### Http请求
* 客户端--发请求--服务器

##### 1.请求行
* 请求行中的请求方式：GET
* 请求方式：GET、POST、HEAD、DELETE、PUT、TRACT
	* get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址显示数据内容，不安全，但高效
	* post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址显示数据内容，安全，但不高效

##### 2.消息头
```
Accept:告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开换式保持连接
HOST：主机
```



### Http响应
* 服务器--响应--客户端

##### 1.响应体
```
Refresh:告诉客户端，多久刷新一次
Location：让网页重新定位
```

##### 2.响应状态码
200：请求响应成功
3XX：请求重定向
* 重定向：你重新到新位置
404：找不到资源
5XX：服务器代码错误
* 502：网关错误


面试题
当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么
