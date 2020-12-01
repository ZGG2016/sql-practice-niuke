# [查找最晚入职员工的所有信息](https://www.nowcoder.com/practice/218ae58dfdcd4af195fff264e062138f?tpId=82&&tqId=29753&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

查找最晚入职员工的所有信息，为了减轻入门难度，目前所有的数据里员工入职的日期都不是同一天(sqlite里面的注释为--,mysql为comment)

```sql
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,  -- '员工编号'
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

	10008   1958-02-19  Saniya       Kalloufi     M     1994-09-15

## 2、题解

【最晚入职的那个(那几个)员工的**所有**信息】

当所有的数据里员工入职的日期都不是同一天：

```sql
-- 1.排序后取limit
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees 
	order by hire_date desc limit 1;
-- 2.窗口函数
```

当所有的数据里员工入职的日期存在是同一天：

```sql
-- 1.max+子查询
select emp_no,birth_date,first_name,last_name,gender,hire_date from employees 
	where hire_date = (select max(hire_date) from employees);
-- 2.窗口函数
```

对max:

	如果只取一个hire_date值，可以直接`select max(hire_date) from employees)`。
	
	如果取所有信息，将max放子查询中。

**取最值，可以排序后取limit，也可以直接max\min，也可以用窗口函数，要注意是取一个值，还是取所有信息。**

## 3、涉及内容

(1)limit、offset

	limit y : 读 y 条数据

	limit x, y : 跳过 x 条数据，读 y 条数据 
	【limit 0,1读第一条，limit 1,1跳过第一条读第二条】

	limit y offset x : 跳过 x 条数据，读 y 条数据

	select * from test limit 30; 
	select * from test limit 30, 30; 
	select * from test limit 30 offset 30; 

(2)ORDER BY 

用于根据指定的列对结果集进行排序。默认升序asc。降序是desc。

(3)[子句查询](https://blog.csdn.net/Noblelxl/article/details/90646648)

