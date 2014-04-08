---
title: 100408 php 关于 sqllite应用
layout: post
permalink: /1012.html
categories:
  - DataBase
tags:
  - 80slife
  - PHP
  - PHP链接sqllite方法
  - sqllite
---
[<img class="aligncenter size-medium wp-image-1013" title="sqllite" src="http://www.80aj.com/wp-content/uploads/2010/04/sqllite-300x251.jpg" alt="" width="300" height="251" />][1]

关于cs客户端的保存 用户信息 一般用的都是sqllite 。这次公司的 模块自由化开发中 需要 用php 帮助生成 数据库 让用户去下载。【具体的话是关于cs异步升级-_-超强概念】

下面是关于一些sqllite介绍 以及php运用方法:

SQLite介绍

自几十年前出现的商业应用程序以来，数据库就成为软件应用程序的主要组成部分。正与数据库管理系统非常关键一样，它们也变得非常庞大，并占用了相当多的系统资源，增加了管理的复杂性。随着软件应用程序逐渐模块模块化，一种新型数据库会比大型复杂的传统数据库管理系统更适应。嵌入式数据库直接在应用程序进程中运行，提供了零配置（zero-configuration）运行模式，并且资源占用非常少。

SQLite是一个开源的嵌入式关系数据库，它在2000年由D. Richard Hipp发布，它的减少应用程序管理数据的开销，SQLite可移植性好，很容易使用，很小，高效而且可靠。

SQLite嵌入到使用它的应用程序中，它们共用相同的进程空间，而不是单独的一个进程。从外部看，它并不像一个RDBMS，但在进程内部，它却是完整的，自包含的数据库引擎。

嵌入式数据库的一大好处就是在你的程序内部不需要网络配置，也不需要管理。因为客户端和服务器在同一进程空间运行。SQLite 的数据库权限只依赖于文件系统，没有用户帐户的概念。SQLite 有数据库级锁定，没有网络服务器。它需要的内存，其它开销很小，适合用于嵌入式设备。你需要做的仅仅是把它正确的编译到你的程序。

PHP 关于  sqllite 使用方法:

> <?php  
> $db=sqlite_open(&#8220;db.sqlite&#8221;); //打开db.sqlite数据库，如果不存在则尝试创建。  
> sqlite_query($db,&#8221;drop table test&#8221;);  
> sqlite_query($db,&#8221;create table test (id INTEGER PRIMARY KEY,name text);&#8221;); //创建test表，id字段为自动递增主键  
> sqlite_query($db,&#8221;insert into test (name) values(&#8216;hello&#8217;);&#8221;); //插入一行内容  
> sqlite_query($db,&#8221;insert into test (name) values(&#8216;world&#8217;);&#8221;);//插入一行内容  
> $result=sqlite_query($db,&#8221;select * from test&#8221;); //取得test表的所有内容  
> while($row=sqlite\_fetch\_array($result)) { //通过while循环表中所有内容  
> print &#8220;<br>&#8221;;  
> print_r($row);  
> print &#8220;<br>&#8221;;  
> }  
> sqlite_close($db);//关闭数据库的连接  
> ?>

百度百科  sqllite：

<http://baike.baidu.com/view/1447600.htm?fr=ala0_1>

 [1]: http://www.80aj.com/wp-content/uploads/2010/04/sqllite.jpg