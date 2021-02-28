# [SQL41：构造一个触发器audit_log，在向employees表中插入一条数据的时候，触发插入相关的数据到audit中](https://www.nowcoder.com/practice/7e920bb2e1e74c4e83750f5c16033e2e?tpId=82&&tqId=29809&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

构造一个触发器 audit_log，在向 employees_test 表中插入一条数据的时候，触发插入相关的数据到 audit 中。

```sql
CREATE TABLE employees_test(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL,
ADDRESS CHAR(50),
SALARY REAL
);
CREATE TABLE audit(
EMP_no INT NOT NULL,
NAME TEXT NOT NULL
);
```

## 2、题解


```sql
CREATE TRIGGER audit_log AFTER INSERT ON employees_test
FOR EACH ROW
BEGIN
INSERT INTO audit VALUES(NEW.ID,NEW.NAME);
END
```

## 3、涉及内容

(1)MYSQL 触发器：

	CREATE TRIGGER trigger_name trigger_time trigger_event ON tbl_name 
	FOR EACH ROW
	BIGIN
	 trigger_stmt
	END

1、trigger_name 标识触发器名称，用户自行指定

2、trigger_time 标识触发时机，可以为 before 或 after

3、trigger_event 标识触发事件，包括 INSERT、UPDATE 和 DELETE

4、tbl_name 标识建立触发器的表名，即在哪张表上建立触发器

5、trigger_stmt 是触发器内容，触发器程序可以使用 begin 和 end 作为开始和结束，中间包含多条语句