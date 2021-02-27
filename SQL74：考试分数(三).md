# [SQL74：考试分数(三)](https://www.nowcoder.com/practice/b83f8b0e7e934d95a56c24f047260d91?tpId=82&&tqId=35494&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

牛客每次举办企业笔试的时候，企业一般都会有不同的语言岗位，比如C++工程师，JAVA工程师，Python工程师，每个用户笔试完有不同的分数，现在有一个分数(grade)表简化如下:
 
![SQL74-1](./image/SQL74-1.png)

第1行表示用户id为1的选择了language_id为1岗位的最后考试完的分数为12000，
....

第7行表示用户id为7的选择了language_id为2岗位的最后考试完的分数为11000，

不同的语言岗位(language)表简化如下:

![SQL74-2](./image/SQL74-2.png)

请你找出每个岗位分数排名前2的用户，得到的结果先按照language的name升序排序，再按照积分降序排序，最后按照grade的id升序排序，得到结果如下:

![SQL74-3](./image/SQL74-3.png)

## 2、题解

注意：排名相同的，一并列出来。

```sql
-- 窗口函数
select a.id,a.name,a.score
from (select g.id,l.name,g.score,
      dense_rank() over(partition by l.name order by g.score desc) dr
      from grade g
      join language l on g.language_id=l.id)a
where a.dr<=2
order by a.name asc,a.score desc,a.id asc;

-- join
-- 取出第二大的分数，再过滤
SELECT
    g.id,
    l.name,
    g.score
FROM
    grade g JOIN LANGUAGE l
    ON g.language_id = l.id
-- 先取第一大的分数
WHERE score >= (SELECT IFNULL(MAX(score),0) FROM grade g2 
                WHERE g2.language_id = g.language_id
               AND score < (SELECT MAX(score) FROM grade g3 
                                 WHERE g3.language_id = g.language_id))
ORDER BY l.name ASC , g.score DESC;
```

## 3、涉及内容

(1)ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

	SELECT column_name,column_name
	FROM table_name
	ORDER BY column_name,column_name ASC|DESC;

注意对多列排序的方式。

	ORDER BY a ASC ,b DESC;