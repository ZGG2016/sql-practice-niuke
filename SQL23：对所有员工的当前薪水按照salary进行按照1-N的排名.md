# [SQL23：对所有员工的当前薪水按照salary进行按照1-N的排名](https://www.nowcoder.com/practice/b9068bfe5df74276bd015b9729eec4bf?tpId=82&&tqId=29775&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

对所有员工的当前(to_date='9999-01-01')薪水按照salary进行按照1-N的排名【降序】，相同salary并列且按照emp_no升序排列

```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
```

## 2、题解


```sql
-- 使用窗口函数
select emp_no,salary,
dense_rank() over(order by salary desc) rank
from salaries
where to_date='9999-01-01';


-- 一个序列：'4'、'3'、'2''1'。 按降序排列，'2'的序号是3，此时在这个序列中大于等于当前值的数量也是3
-- 所以，当降序排列的时候，元素的序号就是大于等于当前值的数量。
-- rank排名：查询表中大于自己薪水的员工的数量（考虑并列：去重）
SELECT 
  s1.emp_no,
  s1.salary,
  (SELECT 
    COUNT(DISTINCT s2.salary) 
  FROM
    salaries s2 
  WHERE s2.to_date = '9999-01-01' 
    AND s2.salary >= s1.salary) AS `rank`  -- 去重：计算并列排名
FROM
  salaries s1 
WHERE s1.to_date = '9999-01-01' 
ORDER BY s1.salary DESC,
  s1.emp_no ;
```

## 3、涉及内容