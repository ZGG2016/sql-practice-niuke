# [SQL66：牛客每个人最近的登录日期(一)](https://www.nowcoder.com/practice/ca274ebe6eac40ab9c33ced3f2223bb2?tpId=82&&tqId=35084&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

牛客每天有很多人登录，请你统计一下牛客每个用户最近登录是哪一天。

有一个登录(login)记录表，简况如下:

![SQL66-1](./image/SQL66-1.png)

第1行表示id为2的用户在2020-10-12使用了客户端id为1的设备登录了牛客网

。。。

第4行表示id为3的用户在2020-10-13使用了客户端id为2的设备登录了牛客网


请你写出一个sql语句查询每个用户最近一天登录的日子，并且按照user_id升序排序，上面的例子查询结果如下:

![SQL66-2](./image/SQL66-2.png)

查询结果表明:

user_id为2的最近的登录日期在2020-10-13

user_id为3的最近的登录日期也是2020-10-13

## 2、题解


```sql
select user_id,max(date) as d
from login
group by user_id  -- 要在组内取最大值，不能使用排序和limit
order by user_id; -- 结果输出是升序

-- 组内取最大值使用窗口函数

-- 窗口函数 dense_rank
select user_id,date as d
from (
select user_id,date,
    dense_rank() over(partition by user_id order by date desc ) dr
from login
) t
where dr =1
order by user_id

-- 窗口函数 last_value
select distinct  -- 注意这里使用了distinct
    user_id,
    -- between unbounded preceding and unbounded following 也可以
    last_value(date) over(partition by user_id order by date rows between current row and unbounded following) as d
from login;

-- 窗口函数 first_value
select distinct
    user_id,
    first_value(date) over(partition by user_id order by date desc rows between unbounded preceding and unbounded following) as d
from login;

-- 窗口函数 nth_value
select distinct
    user_id,
    nth_value(date,1) over(partition by user_id order by date desc rows between unbounded preceding and unbounded following) as d
from login;
```

## 3、涉及内容