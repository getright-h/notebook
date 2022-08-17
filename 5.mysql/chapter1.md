## MYSQL

关系型数据库，以表的形式存储

**实体**

**联系**

一或者多，取决于有几个实体

1. 一对一
2. 一对多（一个人=〉多件事，一件事=〉一个人
   1. 一个相关列是一个主键或者唯一约束
   2. 多，从表
   3. 一，主表
3. 多对多（一个人=〉多件事，一件事=〉多个人
   1. 

  

### 1.建表

#### 1.1字段

`varchar(n)`字符串，以实际长度为准，最大为n

`char(n)` 字符串，长度恒为n



#### 1.2约束

1. 有唯一值，设置**主键约束**`PRIMARY KEY`
2. **唯一约束**  `unique` 唯一，可用为空
3. **非空约束** `not null` 不能为空
4. 默认`default`
5. **自增** `auto_increment` 常和主键一起出现

#### 1.3外键约束

关联两个表，保证引用的完整性

先添加主表，再添加从表

`constraint foreign key(当前表要关联的项) reference 主表名(要关联的项)`



```sql
INSERT INTO employee(emp_id,emp_name,emp_gender,emp_address,emp_phone,emp_join_time,emp_dep_id,emp_major_id) VALUES(1,'zhang3','nan','cd',123123,'1999-1-1',1,2)
```



#### 1.4删表

有约束，要先删除被关联的主表



### 2.操作

#### 2.1增

`INSERT INTO 表名(列名，列名) VALUE('值'，'值'),(),()`

