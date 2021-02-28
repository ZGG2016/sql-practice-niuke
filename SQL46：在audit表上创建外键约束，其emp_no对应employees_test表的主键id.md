# [SQL46：在audit表上创建外键约束，其emp_no对应employees_test表的主键id]()

## 1、题目

在 audit 表上创建外键约束，其 emp_no 对应 employees_test 表的主键 id。
(以下2个表已经创建了)

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
create_date datetime NOT NULL
);

```

## 2、题解


```sql
alter table audit add foreign key (emp_no) references employees_test (id)
```

## 3、涉及内容