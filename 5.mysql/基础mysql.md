## 1.基础

### 1.1字段的数据类型

1. `int` 整数
2. `varchar(len)` 字符串  len最大长度
3. `tinyint(1)` 布尔值



### 1.2字段的标识

1. `PK` 主键 唯一标识
2. `NN` 值不能为空
3. `UQ` 唯一值
4. `AI` 值自动增长



### 1.3sql语句

对大小写不敏感

多列用`,`隔开

1. 查

   ```sql
   
   select * from 表名
   --
   select 列表名 from 表名称
   ```

   1. `order by`  asc升序(默认)，desc降序

   2. `distinct 列名`去重

   3. `between and`范围内

   4. `not in(x,y)`不在指定条件内的x,y

   5. `in(x,y,z)`查询指定的条将为x,y,z 

   6. `like`模糊查询

      1. `%`任意字符
      2. `_`单个字符

   7. `CONSTRAINT xxx FOREIGN KEY(s_class_id) REFERENCES t_Class(c_id)`

      1. ```sql
         [CONSTRAINT <外键名>] FOREIGN KEY 字段名 [，字段名2，…]
         REFERENCES <主表名> 主键列1 [，主键列2，…]
         ```

   8. **聚合函数**

      1. `count`
      2. 。

   9. `group by`

   10. `having`二次判断

   ```
   CREATE TABLE t_Class (
   c_id int PRIMARY KEY,
   c_name VARCHAR(20) NOT NULL UNIQUE
   )
   
   CREATE TABLE t_student (
   s_id int PRIMARY KEY AUTO_INCREMENT,
   s_name VARCHAR(20) UNIQUE,
   s_sex VARCHAR(8) DEFAULT '男',
   s_age int,
   s_class_id int,
   CONSTRAINT xxx FOREIGN KEY(s_class_id) REFERENCES t_Class(c_id)
   )
   
   
   
   ```





1. 增

   ```sql
   insert into table_name (列1,列2) values (值1,值2)
   ```

2. 改

   ```sql
   update table_name set 列名 = 新值 where 列名(uq) = 某值
   ```

3. 删

   ```sql
   delete from table_name where 列名(uq) = 值 
   ```

4. `where` 子句 限定条件

   可使用运算符

5. `and` 与  `or` 或 

6. `order by` 排序 

   默认升序 `asc`

   降序 `desc`

   多重排序 : 一次排序后根据下一个规则对剩下条件相同的项根据第二规则排序

   `select * from table_name order by xx desc,xx asc;`

7. `count(*)`  统计总数

   ```mysql
   select count(*)  from 
   ```

8. `as` 给查询出的结果设置别名

9. `DROP DATABASE XXX`删除数据库xxx

10. `ALERT TABLE XXX ADD 列名 类型 约束`插入新的列

11. `change`

12. ![1648108516308](基础mysql.assets/1648108516308.png)

13. `ALERT` 更改表结构(不要用)

14. `limit n |n,m`筛选n条，或者从n开始的m条 （从1开始计数



#### 1.2 链接

#### 1.2.1 内链接

`a join( b ON 过滤条件) XX join( c ON 过滤条件)`

xx为自定义的前一个join关系后得到的新表，

#### 1.2.2外链接

**左外链接**

以左边的表为主表，主表的所有东西都会被显示

`a left join( b ON 过滤条件) `

**右外链接**

同理

## 2.项目中操作mysql

### 1.配置mysql模块

```js
//导入mysql模块
const mysql = require("mysql");
//建立与mysql库的关系
const db = mysql.createPool({
    host: "127.0.0.1",
    user: "root",
    password: "admin123",
    database: "my_db_01",
});
```



测试：





```js
//测试
 db.query("select 1", (err, res) => {
        if (err) {
        console.log(err.message);
    }
    //只要可以打印 [ RowDataPacket { '1': 1 } ] 就是成功
    console.log(res);
});

```



1. 查询

   若执行语句时 select 则返回数组

   ```js
   db.query(sql语句, (err, res) => {
       if (err) {
           console.log(err.message);
       }
       console.log(res);
   }); 
   ```

2. add

   若执行语句时insert 则返回对象

   ```js
   //1.编辑查询对象
   let user = { username: "zh3ang", password: "9527" };
   //2.编辑查询语句
   //?占位
   let sql = "insert into users (username,password) values(?,?)";
   //3.执行
   //使用数组  给占位符? 添加值
   db.query(sql, [user.username, user.password], (err, res) => {
       if (err) {
           console.log(err.message);
       }
       //判断是否成功
       if (results.affectedRows === 1) {
           console.log("插入成功");
       }
   });
   ```

   便捷写法：

   ```js
   let user = { username: "zh3ang", password: "9527" };
   
   
   // set ?占位
   let sql = "insert into users set ?";
   
   //user
   db.query(sql, user, (err, res) => {
       if (err) {
           console.log(err.message);
       }
       //判断是否成功
       if (results.affectedRows === 1) {
           console.log("插入成功");
       }
   });
   ```

3. 改

   当sql语句中有多个？占位符，要用数组给每个具体占位符指定值

   ```js
   let user = {username:'bill',id:6}
   let sql = 'update users set ? where id = ?'
   db.query(sql,[user,user.id],(err,res) => {
       //code
   })
   ```

4. 删

   只有一个？占位符，就可以直接写值

   ```
   let sql = "delete from users where id = ?";
   db.query(sql, 6, (err, res) => {
       if (err) return console.log(err.message);
       if (res.affectedRows === 1) console.log("删除成功");
   });
   ```

5. 标记删除

   更新status为1 ，不用真正删除

   ```
   let sql = "update users set status = ? where id = ?";
   db.query(sql, [1, 5], (err, res) => {
       if (err) return console.log(err.message);
       if (res.affectedRows === 1) console.log("删除成功");
   });
   ```

   