---
layout: post
title:  SQL Server常用函数
date:   2017-05-05 11:21:32
categories: 数据库
pid: 20170505-185236
image: sqlserver.jpg
---

***

>拆分字符串string_split 

``` sql
select value from string_split(@contactBId,',')
```

***

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

***

>字符串转日期
``` sql
字符串转日期

SELECT CONVERT(datetime,'11/1/2003',101)
-- 字符转换为日期时,Style的使用

--1. Style=101时,表示日期字符串为:mm/dd/yyyy格式
SELECT CONVERT(datetime,'11/1/2003',101)
--结果:2003-11-01 00:00:00.000

--2. Style=101时,表示日期字符串为:dd/mm/yyyy格式
SELECT CONVERT(datetime,'11/1/2003',103)
--结果:2003-01-11 00:00:00.000
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

***

>OVER(PARTITION BY)函数用法

``` sql
-- 分组聚合，取日期内第一条记录
select c.effectStartTime,c.effectEndTime from (
select 
row_number() OVER(PARTITION by b.effectStartTime order by b.effectStartTime) num,
* from (
		select CONVERT(varchar(10), t.effectStartTime, 23) effectStartTime,CONVERT(varchar(10), t.effectEndTime, 23) effectEndTime 
		FROM schemeServiceFee t where t.schemeId = 57 ) b)
		c where c.num = 1
```

***

>stuff  : 实现mysql group_concat效果

``` sql
SELECT
	schemeId,
	STUFF(
		(
			SELECT
				CAST (contentId AS nvarchar(10)) + ','
			FROM
				schemeContent
			WHERE
				schemeId = sc.schemeId FOR XML PATH ('')
		),
		1,
		0,
		''
	) contentId,
	STUFF(
		(
			SELECT
				content + ','
			FROM
				schemeContent
			WHERE
				schemeId = sc.schemeId FOR XML PATH ('')
		),
		1,
		0,
		''
	) content
FROM
	schemeContent sc
GROUP BY
	schemeId
```
``` sql
SELECT STUFF(
		(
			SELECT
				REPLACE(str(subId), ' ', '') + ','
			FROM
				ms_microseer_test.dbo.userSub
			WHERE
				userId = us.userId FOR XML PATH ('')
		),
		1,
		0,
		''
	) userIds FROM  ms_microseer_test.dbo.userSub us WHERE userId = 3082 GROUP BY userId;
```

***

>分页查询 offset 

```sql
SELECT * from bill order by id
offset 1 rows fetch next 10 rows only;

order by columns
offset @start  rows fetch next @limit  rows only
```

***

>强转  cast

``` sql
CAST (expression AS data_type)

SELECT CAST('12' AS int)
```

***

>执行存储过程
``` sql
DECLARE	@return_value int,
		@totalRow nvarchar(36),
@supplierId int = 118,
@page int = 4,
@limit int = 2

EXEC	@return_value = [dbo].[pContactsQueryList] @supplierId,@page,@limit,@totalRow OUTPUT 

SELECT	@totalRow as '@totalRow'

SELECT	'Return Value' = @return_value
```

``` sql
USE [ms_scm_export_test]
GO

DECLARE	@return_value Int,
		@message nvarchar(100)

EXEC	@return_value = [dbo].[pAccountExportPrepareData]
		@exportNum = 123,
		@uid = NULL,
		@fromCompanyName = N'',
		@category = NULL,
		@paymentsType = NULL,
		@status = N'',
		@isDiff = NULL,
		@csId = NULL,
		@paymentsTimeStart = N'2016-12-16',
		@paymentsTimeEnd = N'2017-12-16',
		@message = @message OUTPUT

SELECT	@message as N'@message'

SELECT	@return_value as 'Return Value'

GO
```

***

>连接字符串 concat

``` sql 
concat(str1, str1)

select concat('123', 456)  -- 123456

SELECT '123' + 123  -- 246
```

***

>日期处理函数 DATEADD

```
SQL Server Date 函数
GETDATE() 返回当前日期和时间
DATEPART() 返回日期/时间的单独部分
DATEADD() 在日期中添加或减去指定的时间间隔
DATEDIFF() 返回两个日期之间的时间
CONVERT() 用不同的格式显示日期/时间
```
``` sql
select DATEADD(mm, -1, GETDATE())
```
>定义和用法
DATEADD() 函数在日期中添加或减去指定的时间间隔。
语法
DATEADD(datepart,number,date)
date 参数是合法的日期表达式。number 是您希望添加的间隔数；对于未来的时间，此数是正数，
对于过去的时间，此数是负数。

datepart 参数可以是下列的值：

|datepart|	缩写|
|---|---|
|年|	yy, yyyy|
|季度	|qq, q|
|月	mm, m|
|年中的日|	dy, y|
|日|	dd, d|
|周|	wk, ww|
|星期|	dw, w|
|小时|	hh|
|分钟|	mi, n|
|秒	|ss, s|
|毫秒|	ms|
|微妙|	mcs|
|纳秒	||ns|

***

>取行号 row_number() over(order by id desc)

``` sql
SELECT  row_number() over(order by id desc) as num,t.* from bill t
```

***

>指定当 Transact-SQL 语句产生运行时错误时，Microsoft® SQL Server™ 是否自动回滚当前事务  
>SET XACT_ABORT

```
Transact-SQL 参考
SET XACT_ABORT

指定当 Transact-SQL 语句产生运行时错误时，Microsoft® SQL Server™ 是否自动回滚当前事务。
语法

SET XACT_ABORT { ON | OFF }
注释

当 SET XACT_ABORT 为 ON 时，如果 Transact-SQL 语句产生运行时错误，整个事务将终止并回滚。为 OFF 时，只回滚产生错误的 Transact-SQL 语句，而事务将继续进行处理。编译错误（如语法错误）不受 SET XACT_ABORT 的影响。

对于大多数 OLE DB 提供程序（包括 SQL Server），隐性或显式事务中的数据修改语句必须将 XACT_ABORT 设置为 ON。唯一不需要该选项的情况是提供程序支持嵌套事务时。有关更多信息，请参见分布式查询和分布式事务。

SET XACT_ABORT 的设置是在执行或运行时设置，而不是在分析时设置。
示例

```