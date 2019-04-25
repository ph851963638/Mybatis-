# Mybatis-

1.首先配置Mapper中数据库的查询方法
List<User> getUserBywhere(@Param("u") User user) //接口中的方法
  模糊查询用户编号与用户名称；
<select id="方法名"  resultType="返回结果类型 ">
  select *from user where 
  where 标签可以去掉之后的and 
  <where>    
  <if test="u.uid!=null">
           uid=#{u.uid}           // 用户实体类的属性名
  </if> 
  <if test="u.uname!=null and u.uname!=' '">
          and uname like #{u.uname}
    </if>
 </where>

测试类
              查询用户编号为1的属性
              User user=new User() 
              user.setUid(1);
              List<User> us=um. getUserBywhere(1);
  
  
  
什么是 MyBatis？
     MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

动态SQL
     MyBatis 的强大特性之一便是它的动态 SQL。如果你有使用 JDBC 或其它类似框架的经验，你就能体会到根据不同条件拼接 SQL 语句的痛苦。例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL 这一特性可以彻底摆脱这种痛苦。


二选一的通配符匹配
<select id="findActiveBlogLike"  resultType="Bolg">  id方法名 resultType返回类型
 select  * from Blog where state='active'
 <if test="title!=null">
   AND title like #{title}
   </if>
 <if test="autor!=null and author.name!=null">
   AND author_name like #{author.name}
  </if>
  
  
  
  where 元素只会在至少有一个子元素的条件返回 SQL 子句的情况下才去插入“WHERE”子句。而且，若语句的开头为“AND”或“OR”，where 元素也会将它们去除。
<!--二选一进行匹配-->

 <select id="getUserBywhere" resultType="User">
    select *from users
    <where>
    <if test="u.uid != null">
    and uid=#{u.uid}
    </if>
    <if test="u.uname != null and u.uname!=null">
     uname like #{u.uname}
    </if>
    </where>
    </select>
    
    有时我们不想应用到所有的条件语句，而只想从中择其一项。针对这种情况，MyBatis 提供了 choose 元素，它有点像 Java 中的 switch 语句。
    
 <select id="findActiveBlogLike"  resultType="Blog">
  SELECT * FROM BLOG WHERE state = ‘ACTIVE’
  <choose>
    <when test="title != null">
      AND title like #{title}
    </when>
    <when test="author != null and author.name != null">
      AND author_name like #{author.name}
    </when>
    <otherwise>
      AND featured = 1
    </otherwise>
  </choose>
</select>
    
    User u=new User();
    Map<Integer,user> users=um.getUsersByKey(u);
    Set<Integer> keys =users.keySet();
    for(Integer k:keys){
    system.out.println(k+"="+users.get(k));
    }
    
    
    
    
    
    
    
    
    
  
  
  
  
  
  

