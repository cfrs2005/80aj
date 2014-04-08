---
title: 121130 mysql 优化以及关于时间段查询的demo
layout: post
permalink: /2492.html
categories:
  - DataBase
tags:
  - mysql
  - 优化
  - 优化思路
  - 大数据导出
  - 文档
  - 时间查询
---
某年某月某日工作 完整迁移 90w左右数据 到新系统 有了如下内容: 在实际未做优化前 执行将数据导出 需要 6 hour, 在最终神秘优化后 只需要 20 minute , 中间的区别就不用多说了吧 未加索引 select \* from album where hideornot = '0' and deleteornot = '0' order by id desc limit 0,30000; 17ms 增加索引 select \* from album where hideornot = '0' and deleteornot = '0' order by id desc limit 0,30000; 2.3ms 精确查询返回字段 select id,photo\_albumid,photo\_description,photo\_width, photo\_height,photo\_host,photo\_path,photo\_goodbabyname,photo\_userid,photo\_username,photo\_categoryid from album where hideornot = '0' and deleteornot = '0' order by id desc limit 0,30000; 1.7ms 单个记录查询 select \* from album\_albums where album\_id=29722; 时间: 0.016ms \*30000 480 ms 6分钟 多表查询 select id,photo\_albumid,photo\_description,photo\_width, photo\_height,photo\_host,photo\_path,photo\_goodbabyname,photo\_userid,photo\_username,photo\_categoryid,a.album\_name,a.album\_description from album ,album\_albums as a where hideornot = '0' and deleteornot = '0' and album\_id=a.album\_id order by id desc limit 0,30000; 直接挂掉了。。。别说6分钟了.. &#8212;&#8212;&#8212;&#8212;&#8212;&#8212;- 关于优化 个人觉得。。。可能重建表。。。。select insert 或许会好好好很多 很多 &#8212;&#8212;&#8212;&#8212;&#8212;&#8212; 就此结束吧 不在考虑了 其实上述的是工作记录，好吧 最给力的神秘优化是 我做了一件很很很 2B的事 这么大的量数据 纯sql语句就有300m 我竟然用本地机器去导远程服务器 所以 这个最给力神秘优化 就是 。。将 db 和 程序 放置在同一网络内。。。不管如何 反正我是2了 mysql查询以日期为条件的 系统函数 查询 以下内容为转载: 今天 select \* from 表名 where to\_days(时间字段名) = to\_days(now()); 昨天 SELECT \* FROM 表名 WHERE TO\_DAYS( NOW( ) ) – TO_DAYS( 时间字段名)