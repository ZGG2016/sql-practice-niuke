# [找出所有员工当前具体的薪水salary情况](https://www.nowcoder.com/practice/ae51e6d057c94f6d891735a48d1c2397?tpId=82&&tqId=29760&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

找出所有员工当前(to_date='9999-01-01')具体的薪水salary情况，对于相同的薪水只显示一次,并按照逆序显示。

```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
```

输出描述:

	salary

	94692

	94409

	88958

	88070


## 2、题解

本题只需对salary字段去重取出即可。

如果要取每位员工在当前的工资情况，即同时取emp_no和salary字段，就要另加考虑。


```sql
-- distinct
select distinct salary 
from salaries
where to_date='9999-01-01'
order by salary desc;

-- group by ，相比distinct性能更好
select salary
from salaries
where to_date='9999-01-01'
group by salary
order by salary desc;

-- 同时取emp_no和salary字段
select distinct emp_no,salary 
from salaries where to_date='9999-01-01' 
order by salary desc;
```

