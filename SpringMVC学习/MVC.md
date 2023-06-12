Model （模型）dao，service
View（视图）jsp
Controller （控制器）Servlet


最典型得MVC JSP + Servlet + JavaBean
pojo：User 实体类
vo：视图层


1. 用户发送请求
2. Servlet接收请求数据，并调用对应得业务逻辑方法
3. 业务处理完毕，返回更新后得数据给servlet
4. servlet转向JSP，由JSP来渲染页面
5. 响应给前端更新后得页面

###### Controller
1. 取得表单数据
2. 调用业务逻辑
3. 转向指定的页面

###### Model
1. 业务逻辑
2. 保存数据的状态

###### View
1. 显示页面
