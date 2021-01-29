# [SQL51：查找字符串'10,A,B'](https://www.nowcoder.com/practice/e3870bd5d6744109a902db43c105bd50?tpId=82&&tqId=29819&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 1、题目

查找字符串'10,A,B' 中逗号','出现的次数cnt。

## 2、题解

原来串的长度 - 替换之后的串的长度 就是 被替换的 逗号的个数

```sql
select length("10,A,B")-length(replace("10,A,B",",","")) cnt;
```

## 3、涉及内容

length()和char_length()：用来获取字符串长度。

区别是：

length()： 单位是字节，utf8编码下,一个汉字三个字节，一个数字或字母一个字节。gbk编码下,一个汉字两个字节，一个数字或字母一个字节。

char_length()：单位为字符，不管汉字还是数字或者是字母都算是一个字符。

原文地址：[https://www.cnblogs.com/biehongli/p/12389418.html](https://www.cnblogs.com/biehongli/p/12389418.html)