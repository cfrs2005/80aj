---
title: '091208  postgresql 数据库的 备份 转移 还原'
layout: post
permalink: /813.html
categories:
  - DataBase
tags:
  - POSTGRESQL
  - 备份
  - 数据库
  - 转移
  - 还原
---
 删除某目录 rm -rf /home/newsite/ 进入 postgre管理员账号 su &#8211; postgre 数据库开启: /usr/local/pgsql/bin/postmaster -i -D 【path】  数据库备份： pg_dump dbname | gzip > filename.gz 创建并还原数据库: 创建数据库: createdb -E utf-8 dbname gunzip -c filename.gz | psql dbname   good lucky