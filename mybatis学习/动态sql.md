### if语句
```xml
<!--1=1是必定查出一个-->
select * from user where 1=1
<if test="判断条件">
    SQL语句（and name = #{name}）
</if>
```

### choose、when和otherwise标签

```xml
<!--像switch-->
<choose>
    <when test="判断条件1">
        SQL语句1
    </when >
    <when test="判断条件2">
        SQL语句2
    </when >
    <when test="判断条件3">
        SQL语句3
    </when >
    <otherwise>
        SQL语句4
    </otherwise>
</choose>

```
```xml 示例
<!--    动态sql-->    
<select id="selectAllUser" resultMap="userMap">        
    select * from mybatis.user where  
    <where>
        <choose>            
	        <when test="name != null and name != ''">                
	            AND name LIKE CONCAT('%',#{name},'%')            
	        </when>            
	        <otherwise>               
	            AND pwd is not null            
	        </otherwise>        
	    </choose>    
    </where>
</select>
```

每一条SQL语句中加入了一个条件"1=1"，如果没有这个条件，就会变成一条错误的语句
```sql
SELECT * FROM user AND name LIKE CONCAT('%',#{name},'%')
```

### where
用来处理AND/OR,where会检索语句，它会将where后的第一个SQL条件语句的AND或者OR关键词去掉
```xml
<where>
    <if test="判断条件">
        AND/OR
    </if>
</where>
```
```xml 示例
<!--    动态sql-->    
<select id="selectAllUser" resultMap="userMap">        
    select * from mybatis.user        
    <where>            
        <if test="name != null and name != ''">                
            name like #{name}            
        </if>       
    </where>    
</select>
```

### forEach
```xml
<foreach item="item" index="index" collection="list|array|map key" open="(" separator="," close=")">
    参数值
</foreach>

```

* item：表示本次迭代获取的元素，若collection为List、Set或者数组，则表示其中的元素；若collection为map，则代表key-value的value，该参数为必选
* index：在list、Set和数组中,index表示当前迭代的位置，在map中，index代指是元素的key，该参数是可选项。
* open：表示该语句以什么开始（既然是 in 条件语句，所以必然以(开始）。
* separator：表示在每次进行迭代之间以什么符号作为分隔符（既然是 in 条件语句，所以必然以,作为分隔符）。
* close：表示该语句以什么结束（既然是 in 条件语句，所以必然以)开始）。
* collection表示迭代集合的名称，可以使用@Param注解指定，有以下四种情况
	 1.如果传入的是单参数且参数类型是一个 List，collection 属性值为 list
	 2.如果传入的是单参数且参数类型是一个 array 数组，collection 的属性值为 array；
	 3.如果如果传入的是单参数且参数类型是一个Set集合的时候，可以通过注解@Param("set")指定key值；
	 4.如果传入的参数是多个，需要把它们封装成一个 Map，当然单参数也可以封装成 Map。Map 的 key 是参数名，collection 属性值是传入的 List 或 array 对象在自己封装的 Map 中的 key。必须加上注解@Param指定

##### 查询多个id
```xml
<select id="selectUser" resultMap="userMap">
    SELECT * FROM user
    <foreach item="id" index="index" collection="list" open="and ("
             separator="," close=")">
        id = #{id}
    </foreach>
</select>

```

```java Test类
User user = new User();
user.setId(1)
user.setId(2)
```

### bind 
每个数据库的拼接函数或连接符号都不同，SQL映射文件旧需要根据不同的数据库提供不同的实现，显然比较麻烦，且不利于代码的移植

```xml
<select id="queryUser" resultMap="userMap">
    <bind name="pattern" value="'%'+_parameter+'%'" />
    SELECT * FROM `user`
    WHERE name like #{pattern} 
</select>

```

### trim 
```xml
<trim prefix="前缀" suffix="后缀" prefixOverrides="忽略前缀字符" suffixOverrides="忽略后缀字符">
    SQL语句
</trim>
prefixOverrides : AND | OR

<trim prefix="SET" suffixOverrides=",">
    SQL语句
</trim>
```
```xml
<select id="selectAllUser" resultMap="userMap">
    select * from user
    <trim prefix="where" prefixOverrides="and">
        <if test="name != null">
            and `name` like #{name}
        </if>
    </trim>
</select>

```


### set
```xml
<update>
	update mybatis.blog
	<set>
		<if test="title != null">
			title = #{titile},
		</if>
		<if test="author != null">
			author = #{author}
		</if>
	</set>
	where id = #{id}
</update>
```

### sql片段
```xml
<sql id="if-title-author">
	<if test="title != null">
		title = #{title}
	</if>
</sql>


<!--引用-->
<select>
	select * from user
	<where>
		<include refid="if-title-author"></include>
	</where>
</select>

```

注意事项：
* 最好基于单表来定义SQL片段
* 不要存在where标签