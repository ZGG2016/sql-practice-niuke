# [SQL39：针对上面的salaries表emp_no字段创建索引idx_emp_no，查询emp_no为10005](https://www.nowcoder.com/practice/f9fa9dc1a1fc4130b08e26c22c7a1e5f?tpId=82&&tqId=29807&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

针对 salaries 表 emp_no 字段创建索引 idx_emp_no，查询 emp_no 为 10005，使用强制索引。

```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
create index idx_emp_no on salaries(emp_no);
```

## 2、题解


```sql
select * from salaries force index(idx_emp_no) where emp_no=10005;
```

## 3、涉及内容

强制索引：

	SELECT * FROM <表名> FORCE INDEX (<索引名>)