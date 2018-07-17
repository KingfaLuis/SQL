# select 使用limit 截取查询结果

## 语句通用格式和注意

```mysql
select * from table_name [where 字句] [order by 字句] limit [offset,] rowCount;
#offset：查询结果的起始位置，获取的记录条数
#rowCount是从起始位置开始获取的记录条数
#如果不写limit 后的offset，则默认从0下标开始

# 注意 limit rowCount = limit 0,rowCount;
```

## 用法

假设有这么一张表名叫ids，只有id一列：

```
id
---
1
2
3
4
5
...
...
197
198
199
20012345678910111213
```

执行

```
SELECT * FROM ids LIMIT 10, 11
```

输出：

```
id
---
11123
```

执行

```
SELECT * FROM ids LIMIT 10, 31
```

输出：

```
id
---
11
12
1312345
```

执行

```
SELECT * FROM ids LIMIT 45, 11
```

输出：

```
id
---
46123
```

从以上示例可以看出，LIMIT后的第一个参数是输出记录的初始位置，第二个参数偏移量，偏移多少，输出的条目就是多少。

再看与LIMIT搭配的还有一个OFFSET命令：

执行

```
SELECT * FROM ids LIMIT 10 OFFSET 21
```

输出：

```
id
---
3
4
5
6
7
8
9
10
11
12123456789101112
```

执行

```
SELECT * FROM ids LIMIT 5 OFFSET 21
```

输出：

```
id
---
3
4
5
6
71234567
```

执行

```
SELECT * FROM ids LIMIT 5 OFFSET 101
```

输出：

```
id
---
11
12
13
14
151234567
```

可以看出OFFSET与逗号隔开基本是一样的，唯一的差别就是两个参数的位置前后颠倒了一下。

于是可以考虑这个一个问题：假如某省高考成绩出来了，按照成绩排名，并取出地m名到第n名的学生信息，这时候LIMIT不就可以用上了嘛：

```
SELECT * FROM list ORDER BY score LIMIT m-1, n - m + 1
```