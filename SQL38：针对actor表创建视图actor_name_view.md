# [SQL38：针对actor表创建视图actor_name_view](https://www.nowcoder.com/practice/b9db784b5e3d488cbd30bd78fdb2a862?tpId=82&&tqId=29806&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

针对actor表创建视图actor_name_view，只包含first_name以及last_name两列，并对这两列重新命名，first_name为first_name_v，last_name修改为last_name_v：

```sql
CREATE TABLE  actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update datetime NOT NULL);
```

## 2、题解


```sql
create view actor_name_view as 
select first_name as first_name_v,last_name as last_name_v from actor;
```

## 3、涉及内容