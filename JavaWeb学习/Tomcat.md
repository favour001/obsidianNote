![[Pasted image 20230610130538.png]]


启动和关闭
启动：StartUp.bat
关闭：shutdown.bat

1. java环境必须要配置，Tomcat是依赖java环境
2. 闪退问题：需要配置兼容性
3. 乱码问题，配置文件中设置


配置：conf/server.xml 
可以配置启动的端口号
* tomcat的默认端口号：8080
* mysql：3306
* http:80
* https:443

可以配置主机的名称
* 默认的主机名为：localhost->127.0.0.1
* 默认网站应用存放的位置为：webapps
*webapps 里面的每一个文件夹代表一个应用

请你谈谈网站是如何进行访问的
1. 输入一个域名；回车
2. 检查本机的C盘里的hosts配置文件下有没有这个域名映射
	1. 有，直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问
	2. 没有：去DNS服务器找，找到的话返回，找不到就报错


配置环境

### 3.4发布一个web网站
1. 将自己写的网站，放到服务器（Tomcat）中指定的web应用的文件夹（webapps）下，就可以访问了
```
--webapps:Tomcat服务器的web目录
	- ROOT
	- 自己的项目
		- WEB-INF
			- classes：java
			- lib：web应用所依赖的jar包
			- web.xml
		- index.html 默认的首页
		- static
			- css
				- style.css
			- js
			- img
```