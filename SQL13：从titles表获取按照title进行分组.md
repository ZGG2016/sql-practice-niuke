# [从titles表获取按照title进行分组](https://www.nowcoder.com/practice/72ca694734294dc78f513e147da7821e?tpId=82&&tqId=29765&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

从titles表获取按照title进行分组，每组个数大于等于2，给出title以及对应的数目t。

```sql
CREATE TABLE IF NOT EXISTS "titles" (
`emp_no` int(11) NOT NULL,
`title` varchar(50) NOT NULL,
`from_date` date NOT NULL,
`to_date` date DEFAULT NULL);
```

## 2、题解

```sql
select title,count(*) t
from titles
group by title
having t>=2;
```

## 3、涉及内容

注意where和having的区别

(1)HAVING 子句

在 SQL 中增加 HAVING 子句原因是，**WHERE 关键字无法与聚合函数一起使用**。

HAVING 子句可以让我们**筛选分组后的各组数据**。

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
```

(2)where 和 having 的区别

where 子句的作用是在对查询结果进行分组前，将不符合where条件的行去掉，也就是**在分组之前过滤数据**，条件中不能包含聚和函数，使用where条件限制特定的行。 

having 子句的作用是筛选满足条件的组，即**在分组之后过滤数据**，条件中经常包含聚合函数，使用having 条件过滤特定的组，也可以使用多个分组标准进行分组。

总之一条sql中有where having group by的时候，顺序是 where  group by having

```sql

mysql> SELECT sal from WINDOWFUNC_TEST WHERE sal>3000;
+------+
| sal  |
+------+
| 4000 |
| 6000 |
| 5000 |
+------+
3 rows in set (0.00 sec)

mysql> SELECT sal from WINDOWFUNC_TEST having sal>3000;     
+------+
| sal  |
+------+
| 4000 |
| 6000 |
| 5000 |
+------+
3 rows in set (0.00 sec)

mysql> SELECT dept from WINDOWFUNC_TEST having sal>3000;     
ERROR 1054 (42S22): Unknown column 'sal' in 'having clause'

mysql> SELECT dept from WINDOWFUNC_TEST where sal>3000;      
+------+
| dept |
+------+
| d2   |
| d2   |
| d2   |
+------+
3 rows in set (0.00 sec)

mysql> SELECT DEPT,AVG(SAL) A FROM WINDOWFUNC_TEST GROUP BY DEPT HAVING A>1000;
+------+-----------+
| DEPT | A         |
+------+-----------+
| d1   | 2000.0000 |
| d2   | 5000.0000 |
+------+-----------+
2 rows in set (0.00 sec)

mysql> SELECT DEPT,AVG(SAL) A FROM WINDOWFUNC_TEST WHERE A>1000 GROUP BY DEPT; 
ERROR 1054 (42S22): Unknown column 'A' in 'where clause'
```

不要将应该用在 WHERE 子句中的项，使用 HAVING。例如，不要这么写：

```sql
SELECT col_name FROM tbl_name HAVING col_name > 0;
```

应该这么写：

```sql
SELECT col_name FROM tbl_name WHERE col_name > 0;
```

(3) 

一个 `select_expr` 可以使用 `AS alias_name` 给出一个别名。这个别名用作这个表达式的列名，可以用在 `GROUP BY`、`ORDER BY`、`HAVING` 子句中，不允许在 `WHERE` 子句中引用列别名。

允许 HAVING 去引用 SELECT 中列出的列和外层子查询中的列。

例如：

```sql
SELECT CONCAT(last_name,', ',first_name) AS full_name
  FROM mytable ORDER BY full_name;
```

[select的更多描述](https://github.com/ZGG2016/mysql-reference-manual/blob/master/13%20SQL%20Statements/13.02%20%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E8%AF%AD%E5%8F%A5Data%20Manipulation%20Statements/13.02.10%20SELECT%20Statement/13.02.10%20SELECT%20Statement.md)