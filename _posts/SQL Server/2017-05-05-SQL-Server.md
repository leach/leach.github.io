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