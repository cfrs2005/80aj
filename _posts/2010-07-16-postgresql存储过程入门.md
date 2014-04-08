---
title: 100720 postgresql 存储过程 入门
layout: post
permalink: /1363.html
categories:
  - DataBase
tags:
  - POSTGRESQL
  - 入门
  - 存储过程
---
 对于存储过程我也是一知半解的，前段时间的通宵加班,对postgresql 有了些深入了解，原来老是看别人的教程 老看不明白 , 只有在应用中学习才会更快，这或许是程序员的通病吧。 先读代码后学习结构： CREATE OR REPLACE FUNCTION getroomversion(roomid integer)  //创建或者替换函数getroomversion //输入参数为整形数 RETURNS integer AS  //返回整形,函数开始 $BODY$           //标准用法 正文开始 DECLARE          //定义一个游标,我所谓的变量&#8230;.可能有错误 verid integer; BEGIN           //开始 select version into verid  from rooms where nvcbid=roomid;  //查询房间号 为roomid的房间  字段为version 的值 插入到 verid里面去 IF NOT FOUND THEN   // 如果不存在 RETURN -1;           //返回-1 END IF;            //if 判断结束 RETURN verid;      //返回 verid END;       //结束 $BODY$    //正文结束 LANGUAGE &#8216;plpgsql&#8217; VOLATILE;//postgresql必定结尾 简单的代码阅读完以后 我们来看下结构 首先说一下 整个的结构 postgresql 不像其他数据库使用的是 procedure postgresql 用的是function 平时创建可以是  create function \*** 函数名 或者 和我一样这样写 CREATE OR REPLACE FUNCTION getroomsversion 函数名后面可以加参数 一般格式是  变量名,变量类型,采用数据库类型 如 roomid integer roomname character varying 可以在前面再加前缀 提示是输入还是输出, 这一句是我猜测的! IN  roomid integer OUT roomid integer 或者可以直接 integer 调用的时候用 $1 $2  以此类推 存储过程中的赋值: i := 0;       := 为赋值符号 循环: while i<10 loop i := i+1; end loop; For循环 for re in execute &#8216;select name from tableid where id>10&#8242; loop execute &#8216;delete from &#8216;||re.name; end loop; return; 字符串连接用的是|| If判断: if found then continue; else end if 报告错误退出 事务 RAISE EXCEPTION &#8216;update error!&#8217;;  //可以赋值自己想要的报错内容 具体文档提示： http://www.pgsqldb.org/pgsqldoc-7.2c/plpgsql-errors-and-messages.html 游标： DECLARE 具体文档提示： http://www.kuqin.com/postgreSQL8.1_doc/sql-declare.html 更多内容请访问： http://www.pgsqldb.org/pgsqldoc-7.2c/index.html 本文系原创转载请注明：blog.80aj.com  80后程序员博客 可乐烟著