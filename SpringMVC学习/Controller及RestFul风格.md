- 控制器复杂提供访问应用程序的行为，通常通过接口定义或注解定义两种方法实现
- 控制器负责解析用户的请求并将其转换为一个模型
- 在Spring MVC中一个控制器类可以包含多个方法
- 在Spring MVC中，对于Controller的配置方式有很多种


## 第一种 Controller


## 第二种 使用注解


```xml
<context:component-scan base-package="com.test.controller"/>  
<!-- 让Spring MVC不处理静态资源 .css .js .html .mp3 .mp4-->
<mvc:default-servlet-handler/>  
<!--  
支持mvc注解驱动  
在spring中一般采用@RequestMapping注解来完成映射关系  
要想使@RequestMapping注解生效  
必须向上下文中注册DefaultAnnotationHandleMapping  
和一个AnnotationMethodHandlerAdapter实例  
这两个实例分别在类级别和方法级别处理  
而annotation-driven配置帮助我们自动完成上述两个实例的注入  
-->  
<mvc:annotation-driven/>
```

```java
@Component   组件
@Service     service
@Controller  controller
@Respository dao
```
