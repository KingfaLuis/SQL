# insert into 与select 组合使用

.一般用法和组合用法

```mysql
#一般用法
insert into [表名] values(值1，值2)
insert into [表名] (列1,列2) values(值1，值2)
#组合用法
Insert into [表名1] select 列1,列2 from [表名2]
Insert into [表名1] (列1,列2) select 列3,列4 from [表名2]

```

1. ## 使用常量插入单个元组  

   格式为：      

   INSERT      INTO〈表名〉[(〈属性列1〉[，〈属性列2〉…)]      VALUES (〈常量1〉[，〈常量2〉]…)； 

应用：平时做数据迁移的时候使用得比较多

### 【例】

将一个新学生记录(学号：‘98010’，姓名：‘张三’，年龄：20，所在系：‘计算机系’ )插入到学生表中。

INSERT  INTO 学生  VALUES (‘98010’，‘张三’，20，‘计算机系’)；

### 【例】

插入一条选课记录(学号：'98011'，课程号：'C10'，成绩不详)。

INSERT   INTO 选课 (学号，课程号)   VALUES ('98011'，'C10')；

2. ## 在表中插入子查询的结果集 

​         INSERT    INTO〈表名〉[(〈属性列1〉[，〈属性列2〉]…)]   〈子查询〉；

### 【例】

求每个系学生的平均年龄，把结果存入数据库中。

  CREATE TABLE 系平均年龄 (系名称CHAR(20)，  平均年龄SMALLINT)；   INSERT  INTO 系平均年龄SELECT 所在系，AVG(ALL年龄)   FROM 学生   GROUP BY 所在系；

[1]: https://www.w3schools.com/sql/sql_insert.asp	"SQL INSERT INTO Statement"

