# [SQL40：在last_update后面新增加一列名字为create_date](https://www.nowcoder.com/practice/119f04716d284cb7a19fba65dd876b03?tpId=82&&tqId=29808&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

存在 actor 表，包含如下列信息：

```sql
CREATE TABLE  actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  datetime NOT NULL);
```

现在在 last_update 后面新增加一列名字为 create_date，类型为 datetime NOT NULL，默认值为 '2020-10-01 00:00:00'

## 2、题解


```sql
alter table actor add column
create_date datetime NOT NULL DEFAULT '2020-10-01 00:00:00'
```

## 3、涉及内容