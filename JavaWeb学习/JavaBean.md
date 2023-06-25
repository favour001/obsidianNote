实体类
JavaBean有特定的写法:
* 必须要有一个无参构造
* 属性必须私有化
* 必须有对应的get/set方法
一般用来和数据库的字段映射
ORM：对象关系映射
* 表 ---> 类
* 字段--->属性
* 行记录--->对象


实体类 一般都和数据库中的表结构一一对应

```jsp
<jsp:userBean id="" class=""></jsp:userBean>

<%--设置属性--%>
<jsp:setProperty name="" property="" value=""/>

<%--获取属性--%>
<jsp:getProperty name="" property=""/>
```