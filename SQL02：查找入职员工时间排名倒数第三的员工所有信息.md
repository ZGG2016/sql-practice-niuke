# [查找入职员工时间排名倒数第三的员工所有信息](https://www.nowcoder.com/practice/ec1ca44c62c14ceb990c3c40def1ec6c?tpId=82&&tqId=29754&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

查找入职员工时间排名倒数第三的员工所有信息，为了减轻入门难度，目前所有的数据里员工入职的日期都不是同一天

```sql
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));
```

输入描述:

无

输出描述:

	emp_no	birth_date	first_name	last_name	gender	hire_date

	10005   1955-01-21   Kyoichi     Maliniak     M    1989-09-12


## 2、题解

当所有的数据里员工入职的日期都不是同一天：

```sql
-- 1.子查询
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees 
	order by hire_date desc limit 2,1;  # 注意这里是2

-- 2.窗口函数
select emp_no,birth_date,first_name,last_name,gender,hire_date 
from (
	select emp_no,birth_date,first_name,last_name,gender,hire_date,
	row_number() over (order by hire_date desc) r
	from employees) e
where r=3;
```

当所有的数据里员工入职的日期存在是同一天：

```sql
-- 1.子查询（distinct、group by）
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees 
    where hire_date = (select distinct hire_date from employees order by hire_date desc limit 2,1);
-- group by 比 distinct 效率更高
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees where hire_date = 
(select hire_date from employees group by hire_date order by hire_date desc limit 2,1)

-- 2.窗口函数，和row_number的区别
select emp_no,birth_date,first_name,last_name,gender,hire_date 
from (
	select emp_no,birth_date,first_name,last_name,gender,hire_date,
	dense_rank() over (order by hire_date desc) dr
	from employees) e
where dr=3;
```

## 3、涉及内容

(1)distinct和group by区别

都可以去重。

位置：

	distinct要放在select后，from前；
	group by放在from后；

执行顺序：
	
	distinct在select后执行；
	group by在from后执行，要比distinct先执行。

功能：

	distinct是去重语句，根据后面的字段去重；
	group by是分组语句，根据后面的字段分组，作用是分组后执行聚合操作。
			分组后，只取分组字段就达到了去重的效果。

性能：

	数据量大的情况下，group by要比distinct效率高些，distinct会进行全表扫描【未测试】


```sql
mysql> select * from access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |     3 | 2016-05-10 |
|   2 |       3 |     2 | 2016-05-13 |
|   3 |       1 |     5 | 2016-05-14 |
|   4 |       2 |     4 | 2016-05-14 |
|   5 |       5 |     4 | 2016-05-14 |
|   6 |       5 |     5 | 2016-05-12 |
|   6 |       1 |     1 | 9999-12-12 |
|   6 |       5 |     5 | 2016-05-12 |
+-----+---------+-------+------------+
8 rows in set (0.00 sec)

mysql> select aid,site_id from access_log group by aid,site_id;
+-----+---------+
| aid | site_id |
+-----+---------+
|   1 |       1 |
|   2 |       3 |
|   3 |       1 |
|   4 |       2 |
|   5 |       5 |
|   6 |       5 |
|   6 |       1 |
+-----+---------+
7 rows in set (0.00 sec)

mysql> select distinct aid,site_id from access_log;
+-----+---------+
| aid | site_id |
+-----+---------+
|   1 |       1 |
|   2 |       3 |
|   3 |       1 |
|   4 |       2 |
|   5 |       5 |
|   6 |       5 |
|   6 |       1 |
+-----+---------+
7 rows in set (0.00 sec)
```

