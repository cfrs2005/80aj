---
title: 100720 postgresql 存储过程 入门
layout: post
permalink: /1363.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292204847";s:13:"related_posts";s:503:"<ul class="related_post"><li><a href="http://blog.80aj.com/2010/12/05/101205-postgresql-update-%e8%a7%a6%e5%8f%91%e5%99%a8/" title="101205 postgresql update 触发器">101205 postgresql update 触发器</a></li><li><a href="http://blog.80aj.com/2009/12/08/091208-postgresql-%e6%95%b0%e6%8d%ae%e5%ba%93%e7%9a%84-%e5%a4%87%e4%bb%bd-%e8%bd%ac%e7%a7%bb-%e8%bf%98%e5%8e%9f-2/" title="091208  postgresql 数据库的 备份 转移 还原">091208  postgresql 数据库的 备份 转移 还原</a></li></ul>";}'
bot_views:
  - 221
views:
  - 588
duoshuo_thread_id:
  - 1280248249638191219
categories:
  - DataBase
tags:
  - POSTGRESQL
  - 入门
  - 存储过程
---
<p style="text-align: center;">
  <a href="http://www.80aj.com/wp-content/uploads/2010/07/postgresql.jpg"><img class="aligncenter size-full wp-image-1364" title="postgresql" src="http://www.80aj.com/wp-content/uploads/2010/07/postgresql.jpg" alt="" width="154" height="212" /></a>
</p>

<div id="_mcePaste">
  对于存储过程我也是一知半解的，前段时间的通宵加班,对postgresql 有了些深入了解，原来老是看别人的教程 老看不明白 , 只有在应用中学习才会更快，这或许是程序员的通病吧。
</div>

<div id="_mcePaste">
  <span style="color: #ff0000;">先读代码后学习结构：</span>
</div>

<div id="_mcePaste">
  CREATE OR REPLACE FUNCTION getroomversion(roomid integer)  //创建或者替换函数getroomversion //输入参数为整形数
</div>

<div id="_mcePaste">
  RETURNS integer AS  //返回整形,函数开始
</div>

<div id="_mcePaste">
  $BODY$           //标准用法 正文开始
</div>

<div id="_mcePaste">
  DECLARE          //定义一个游标,我所谓的变量&#8230;.可能有错误
</div>

<div id="_mcePaste">
  verid integer;
</div>

<div id="_mcePaste">
  BEGIN           //开始
</div>

<div id="_mcePaste">
  select version into verid  from rooms where nvcbid=roomid;  //查询房间号 为roomid的房间  字段为version 的值 插入到 verid里面去
</div>

<div id="_mcePaste">
  IF NOT FOUND THEN   // 如果不存在
</div>

<div id="_mcePaste">
  RETURN -1;           //返回-1
</div>

<div id="_mcePaste">
  END IF;            //if 判断结束
</div>

<div id="_mcePaste">
  RETURN verid;      //返回 verid
</div>

<div id="_mcePaste">
  END;       //结束
</div>

<div id="_mcePaste">
  $BODY$    //正文结束
</div>

<div id="_mcePaste">
  LANGUAGE &#8216;plpgsql&#8217; VOLATILE;//postgresql必定结尾
</div>

<div id="_mcePaste">
  <span style="color: #ff0000;">简单的代码阅读完以后 我们来看下结构</span>
</div>

<div id="_mcePaste">
  <span style="color: #ff0000;">首先说一下 整个的结构</span>
</div>

<div>
  <span style="color: #ff0000;"><br /> </span>
</div>

<div id="_mcePaste">
  postgresql 不像其他数据库使用的是 procedure
</div>

<div id="_mcePaste">
  postgresql 用的是function
</div>

<div id="_mcePaste">
  平时创建可以是  create function *** 函数名
</div>

<div id="_mcePaste">
  或者 和我一样这样写
</div>

<div id="_mcePaste">
  CREATE OR REPLACE FUNCTION getroomsversion
</div>

<div id="_mcePaste">
  函数名后面可以加参数 一般格式是  变量名,变量类型,采用数据库类型
</div>

<div id="_mcePaste">
  如
</div>

<div id="_mcePaste">
  roomid integer
</div>

<div id="_mcePaste">
  roomname character varying
</div>

<div id="_mcePaste">
  可以在前面再加前缀 提示是输入还是输出, 这一句是我猜测的!
</div>

<div id="_mcePaste">
  IN  roomid integer
</div>

<div id="_mcePaste">
  OUT roomid integer
</div>

<div id="_mcePaste">
  或者可以直接
</div>

<div id="_mcePaste">
  integer
</div>

<div id="_mcePaste">
  调用的时候用 $1 $2  以此类推
</div>

<div id="_mcePaste">
  存储过程中的赋值:
</div>

<div id="_mcePaste">
  i := 0;       := 为赋值符号
</div>

<div id="_mcePaste">
  循环:
</div>

<div id="_mcePaste">
  while i<10 loop
</div>

<div id="_mcePaste">
  i := i+1;
</div>

<div id="_mcePaste">
  end loop;
</div>

<div id="_mcePaste">
  For循环
</div>

<div id="_mcePaste">
  for re in execute &#8216;select name from tableid where id>10&#8242; loop
</div>

<div id="_mcePaste">
  execute &#8216;delete from &#8216;||re.name;
</div>

<div id="_mcePaste">
  end loop;
</div>

<div id="_mcePaste">
  return;
</div>

<div id="_mcePaste">
  字符串连接用的是||
</div>

<div id="_mcePaste">
  If判断:
</div>

<div id="_mcePaste">
  if found then
</div>

<div id="_mcePaste">
  continue;
</div>

<div id="_mcePaste">
  else
</div>

<div id="_mcePaste">
  end if
</div>

<div id="_mcePaste">
  报告错误退出 事务
</div>

<div id="_mcePaste">
  RAISE EXCEPTION &#8216;update error!&#8217;;  //可以赋值自己想要的报错内容
</div>

<div id="_mcePaste">
  具体文档提示：
</div>

<div id="_mcePaste">
  http://www.pgsqldb.org/pgsqldoc-7.2c/plpgsql-errors-and-messages.html
</div>

<div id="_mcePaste">
  游标：
</div>

<div id="_mcePaste">
  DECLARE
</div>

<div id="_mcePaste">
  具体文档提示：
</div>

<div id="_mcePaste">
  http://www.kuqin.com/postgreSQL8.1_doc/sql-declare.html
</div>

更多内容请访问：

<http://www.pgsqldb.org/pgsqldoc-7.2c/index.html>

本文系原创转载请注明：blog.80aj.com  80后程序员博客 可乐烟著