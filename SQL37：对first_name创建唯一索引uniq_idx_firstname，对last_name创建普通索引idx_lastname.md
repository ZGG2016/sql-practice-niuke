# [SQL37：对first_name创建唯一索引uniq_idx_firstname，对last_name创建普通索引idx_lastname](https://www.nowcoder.com/practice/e1824daa0c49404aa602cf0cb34bdd75?tpId=82&&tqId=29805&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

针对如下表 actor 结构创建索引：

(注:在 SQLite 中，除了重命名表和在已有的表中添加列，ALTER TABLE 命令不支持其他操作，mysql 支持 ALTER TABLE 创建索引)

```sql
CREATE TABLE actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  datetime NOT NULL);
```

对 first_name 创建唯一索引 uniq_idx_firstname，对 last_name 创建普通索引idx_lastname

## 2、题解


```sql
alter table actor add unique uniq_idx_firstname (first_name);
alter table actor add index idx_lastname (last_name);
```

## 3、涉及内容

(1)MySQL创建索引

ALTER TABLE 创建索引

添加主键

	ALTER TABLE tbl_name ADD PRIMARY KEY (col_list);
	// 该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL。

添加唯一索引

	ALTER TABLE tbl_name ADD UNIQUE index_name (col_list);
	// 这条语句创建索引的值必须是唯一的。

添加普通索引

	ALTER TABLE tbl_name ADD INDEX index_name (col_list);
	// 添加普通索引，索引值可出现多次。

添加全文索引

	ALTER TABLE tbl_name ADD FULLTEXT index_name (col_list);
	// 该语句指定了索引为 FULLTEXT ，用于全文索引。


使用 CREATE 语句创建索引

	CREATE INDEX index_name ON table_name(column_name,column_name)
	普通索引

	CREATE UNIQUE INDEX index_name ON table_name (column_name) ;

	CREATE TABLE tb_stu_info (
  		id INT NOT NULL [PRIMARY KEY],
		...
  		height INT DEFAULT NULL,
  		[UNIQUE]INDEX(height)
	)

	MySQL 里 Create Index 不能创建主键 Primary Key

删除索引的语法：

	DROP INDEX index_name ON tbl_name;
	// 或者
	ALTER TABLE tbl_name DROP INDEX index_name；
	ALTER TABLE tbl_name DROP PRIMARY KEY;