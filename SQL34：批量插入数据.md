# [SQL34：批量插入数据](https://www.nowcoder.com/practice/51c12cea6a97468da149c04b7ecf362e?tpId=82&&tqId=29802&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

题目已经先执行了如下语句:

```sql
drop table if exists actor;
CREATE TABLE actor (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  DATETIME NOT NULL)
```

请你对于表 actor 批量插入如下数据(不能有 2 条 insert 语句哦!)

actor_id | first_name | last_name | last_update
---|:---|:---|:---
1 | PENELOPE | GUINESS | 2006-02-15 12:34:33
2 | NICK | WAHLBERG | 006-02-15 12:34:33

## 2、题解


```sql
insert into actor (actor_id,first_name,last_name,last_update) 
values (1,'PENELOPE','GUINESS','2006-02-15 12:34:33'),
(2,'NICK','WAHLBERG','2006-02-15 12:34:33');
```

## 3、涉及内容