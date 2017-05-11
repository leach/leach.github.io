---
layout: post
title:  SQL Server常用函数
date:   2017-05-05 11:21:32
categories: 数据库
pid: 20170505-185236
image: sqlserver.jpg
---

>拆分字符串string_split 

``` sql
select value from string_split(@contactBId,',')
```

>sql server解析json 

``` sql
Select * from openJson('
[
  {
     "name": "huang",
     "netname": "HTL",
     "age": 5,
     "isman":true     
  },
{
     "name": "huang1",
     "netname": "HTL1",
     "age": 6,
     "isman":true     
  }
]
') 
WITH(
	name varchar(20) '$.name',
	netname varchar(20) '$.netname',
	age varchar(20) '$.age',
	isman varchar(20) '$.isman',
	remark varchar(20) '$.remark'
)
```

>日期格式化为字符串 convert

``` sql
-- CONVERT() 函数是把日期转换为新数据类型的通用函数。
-- CONVERT() 函数可以用不同的格式显示日期/时间数据。
-- 常用：
Select CONVERT(varchar(100), GETDATE(), 8)  -- 10:57:46
Select CONVERT(varchar(100), GETDATE(), 24) -- 10:57:47
Select CONVERT(varchar(100), GETDATE(), 108) --  10:57:49
Select CONVERT(varchar(100), GETDATE(), 12) -- 060516
Select CONVERT(varchar(100), GETDATE(), 23)  --  2006-05-16  

SELECT CONVERT(varchar(100), GETDATE(), 23)   -- 2017-03-02
SELECT CONVERT(varchar(6), GETDATE(), 112)   -- 201703

-- 全部
Select CONVERT(varchar(100), GETDATE(), 0)   --  05 16 2006 10:57AM
Select CONVERT(varchar(100), GETDATE(), 1)   --  05/16/06
Select CONVERT(varchar(100), GETDATE(), 2)   --  06.05.16
Select CONVERT(varchar(100), GETDATE(), 3)   --  16/05/06
Select CONVERT(varchar(100), GETDATE(), 4)   --  16.05.06
Select CONVERT(varchar(100), GETDATE(), 5)   --  16-05-06
Select CONVERT(varchar(100), GETDATE(), 6)   --  16 05 06
Select CONVERT(varchar(100), GETDATE(), 7)   --  05 16, 06
Select CONVERT(varchar(100), GETDATE(), 8)   --  10:57:46
Select CONVERT(varchar(100), GETDATE(), 9)   --  05 16 2006 10:57:46:827AM
Select CONVERT(varchar(100), GETDATE(), 10)   --  05-16-06
Select CONVERT(varchar(100), GETDATE(), 11)   --  06/05/16
Select CONVERT(varchar(100), GETDATE(), 12)   --  060516
Select CONVERT(varchar(100), GETDATE(), 13)   --  16 05 2006 10:57:46:937
Select CONVERT(varchar(100), GETDATE(), 14)   --  10:57:46:967
Select CONVERT(varchar(100), GETDATE(), 20)   --  2006-05-16 10:57:47
Select CONVERT(varchar(100), GETDATE(), 21)   --  2006-05-16 10:57:47.157
Select CONVERT(varchar(100), GETDATE(), 22)   --  05/16/06 10:57:47 AM
Select CONVERT(varchar(100), GETDATE(), 23)   --  2006-05-16
Select CONVERT(varchar(100), GETDATE(), 24)   --  10:57:47
Select CONVERT(varchar(100), GETDATE(), 25)   --  2006-05-16 10:57:47.250
Select CONVERT(varchar(100), GETDATE(), 100)   --  05 16 2006 10:57AM
Select CONVERT(varchar(100), GETDATE(), 101)   --  05/16/2006
Select CONVERT(varchar(100), GETDATE(), 102)   --  2006.05.16
Select CONVERT(varchar(100), GETDATE(), 103)   --  16/05/2006
Select CONVERT(varchar(100), GETDATE(), 104)   --  16.05.2006
Select CONVERT(varchar(100), GETDATE(), 105)   --  16-05-2006
Select CONVERT(varchar(100), GETDATE(), 106)   --  16 05 2006
Select CONVERT(varchar(100), GETDATE(), 107)   --  05 16, 2006
Select CONVERT(varchar(100), GETDATE(), 108)   --  10:57:49
Select CONVERT(varchar(100), GETDATE(), 109)   --  05 16 2006 10:57:49:437AM
Select CONVERT(varchar(100), GETDATE(), 110)   --  05-16-2006
Select CONVERT(varchar(100), GETDATE(), 111)   --  2006/05/16
Select CONVERT(varchar(100), GETDATE(), 112)   --  20060516
Select CONVERT(varchar(100), GETDATE(), 113)   --  16 05 2006 10:57:49:513
Select CONVERT(varchar(100), GETDATE(), 114)   --  10:57:49:547
Select CONVERT(varchar(100), GETDATE(), 120)   --  2006-05-16 10:57:49
Select CONVERT(varchar(100), GETDATE(), 121)   --  2006-05-16 10:57:49.700
Select CONVERT(varchar(100), GETDATE(), 126)   --  2006-05-16T10:57:49.827
Select CONVERT(varchar(100), GETDATE(), 130)   --  18 ???? ?????? 1427 10:57:49:907AM
Select CONVERT(varchar(100), GETDATE(), 131)   --  18/04/1427 10:57:49:920AM
```
***
>查找字符串 CHARINDEX

``` sql
-- 类似indexOf
SELECT CHARINDEX('.', 'ab.cd.efghi')  -- 3
-- 类似lastIndexOf
SELECT LEN('ab.cd.efg') - CHARINDEX('.', REVERSE('ab.cd.efg')) + 1 -- 6
-- LEN 取字符串长度
SELECT LEN('ab.cd.efg')   -- 9
```
***
>取两个时间差 DATEDIFF
``` sql
DATEDIFF
返回跨两个指定日期的日期和时间边界数。 
-- 语法
DATEDIFF ( datepart , startdate , enddate ) 

-- 示例
SELECT DATEDIFF(yyyy , convert(datetime, '2017-09-08', 20), convert(datetime, '2011-09-08', 20))  --  -6
SELECT DATEDIFF(dd, convert(datetime, '2017-09-08', 20), convert(datetime, '2017-09-18', 20)) -- 10
```
-- 参数  
 datepart

|日期部分|缩写|
| --- | --- |
|year |yy, yyyy |
|quarter| qq, q| 
|Month |mm, m |
|dayofyear |dy, y| 
|Day| dd, d |
|Week| wk, ww |
|Hour| hh |
|minute| mi, n |
|second |ss, s |
|millisecond | ms|