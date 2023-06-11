1. 在javaweb开发中，需要使用大量的jar包，我们手动去导入
2. 如何能够让一个东西自己帮我导入和配置这个jar包

Maven的核心思想：约定大于配置
* 有约束，不要去违反
Maven会规定好你该如何去编写我们的java代码


### 配置环境变量


### 阿里云镜像

在settings.xml 修改
* 镜像：mirror
```xml
 <!-- 中央仓库在中国的镜像 -->
        <mirror>
            <id>nexus-aliyun</id>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
            <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>
        </mirror>

```


* 本地仓库：
```xml
<localRepository>你的路径</localRepository>
```

### 在IDEA中使用Maven

等待资源导入 -> 从阿里云服务器自动下载
![[Pasted image 20230611212508.png]]


标记文件
![[Pasted image 20230611213111.png]]


Tomcat服务的配置

![[Pasted image 20230611214150.png]]


### IDEA侧边栏
![[Pasted image 20230611214530.png]]

### pom文件
pom文件是maven的配置文件

![[Pasted image 20230611215228.png]]
![[Pasted image 20230611215404.png]]


web.xml配置
![[Pasted image 20230611222255.png]]