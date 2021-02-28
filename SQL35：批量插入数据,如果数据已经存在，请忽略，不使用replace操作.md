# [SQL35：批量插入数据，如果数据已经存在，请忽略，不使用replace操作](https://www.nowcoder.com/practice/153c8a8e7805400ba8e384e03acc6b3e?tpId=82&&tqId=29803&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

题目已经先执行了如下语句:

```sql
drop table if exists actor;
CREATE TABLE actor (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  DATETIME NOT NULL);
insert into actor values ('3', 'WD', 'GUINESS', '2006-02-15 12:34:33');
```

对于表 actor 插入如下数据，如果数据已经存在，请忽略(不支持使用 replace 操作)

actor_id | first_name | last_name | last_update
---|:---|:---|:---
'3' | 'ED' | 'CHASE' | '2006-02-15 12:34:33'

## 2、题解


```sql
insert ignore into actor (actor_id,first_name,last_name,last_update)
values (3,'ED','CHASE','2006-02-15 12:34:33');
```

## 3、涉及内容

[mysql中常用的三种插入数据的语句:](https://www.cnblogs.com/stevin-john/p/4768904.html)


	insert into

表示插入数据，数据库会检查主键（PrimaryKey），如果出现重复会报错；

	replace into 

表示插入替换数据，需求表中有 PrimaryKey，或者 unique 索引的话，如果数据库已经存在数据，则用新数据替换，如果没有数据效果则和 insert into 一样。有三种形式：

	1. replace into tbl_name(col_name, ...) values(...)

	2. replace into tbl_name(col_name, ...) select ...

	3. replace into tbl_name set col_name=value, ...
 
insert ignore 表示，如果中已经存在相同的记录，则忽略当前新数据；