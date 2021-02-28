# [SQL44：将id=5以及emp_no=10001的行数据替换成id=5以及emp_no=10005,其他数据保持不变，使用replace实现。](https://www.nowcoder.com/practice/2bec4d94f525458ca3d0ebf3bc8cd240?tpId=82&&tqId=29812&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

将 id=5 以及 emp_no=10001 的行数据替换成 id=5 以及 emp_no=10005，其他数据保持不变，使用 replace 实现，直接使用 update 会报错了。

```sql
CREATE TABLE titles_test (
   id int(11) not null primary key,
   emp_no  int(11) NOT NULL,
   title  varchar(50) NOT NULL,
   from_date  date NOT NULL,
   to_date  date DEFAULT NULL);
 
insert into titles_test values
('1', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('2', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('3', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('4', '10004', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('5', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('6', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('7', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01');
```

## 2、题解


```sql
update titles_test set emp_no=replace(emp_no,10001,10005)
where id=5;
```

## 3、涉及内容

	REPLACE ( string_expression , string_pattern , string_replacement )

参数

string_expression 要搜索的字符串表达式,可以是字符或二进制数据类型。

string_pattern 是要查找的子字符串,可以是字符或二进制数据类型。string_pattern 不能是空字符串 ('')。

string_replacement 替换字符串,可以是字符或二进制数据类型。