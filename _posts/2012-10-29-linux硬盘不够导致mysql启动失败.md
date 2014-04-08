---
title: 121029 linux 硬盘不够 导致mysql启动失败
layout: post
permalink: /2374.html
categories:
  - DataBase
tags:
  - mysql启动失败
  - Starting MySQL.Manager of pid-file quit without updating file
  - 硬盘不够
  - 解决
---
 前段时间在服务器上装了squid 没怎么管，最近这2天挂了 上服务器一看 原来是服务器硬盘全让cache吃了. 启动lnmp 用来web管理服务端 结果 服务器启动mysql 失败. 果断命令得删除缓存后. mysql依然无法启动. 报错代码: Starting MySQL.Manager of pid-file quit without updating file.[FAILED] 网上搜索了下解决办法： ps -A|grep mysql 12931 ? 00:00:00 mysqld_safe 13034 ? 00:00:00 mysqld kill -9 12931 kill -9 13034 ./lnmp restart