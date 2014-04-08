---
title: '091208  postgresql 数据库的 备份 转移 还原'
layout: post
permalink: /813.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292212834";s:13:"related_posts";s:433:"<ul class="related_post"><li><a href="http://blog.80aj.com/2010/12/05/101205-postgresql-update-%e8%a7%a6%e5%8f%91%e5%99%a8/" title="101205 postgresql update 触发器">101205 postgresql update 触发器</a></li><li><a href="http://blog.80aj.com/2010/07/16/100720-postgresql-%e5%ad%98%e5%82%a8%e8%bf%87%e7%a8%8b-%e5%85%a5%e9%97%a8/" title="100720 postgresql 存储过程 入门">100720 postgresql 存储过程 入门</a></li></ul>";}'
bot_views:
  - 192
duoshuo_thread_id:
  - 1280248249638191138
views:
  - 7
categories:
  - DataBase
tags:
  - POSTGRESQL
  - 备份
  - 数据库
  - 转移
  - 还原
---
[<img class="aligncenter size-full wp-image-740" title="pg" src="http://www.80aj.com/wp-content/uploads/2009/12/pg.jpg" alt="pg" width="493" height="338" />][1]  
删除某目录  
rm -rf /home/newsite/

进入 postgre管理员账号  
su &#8211; postgre

数据库开启:  
/usr/local/pgsql/bin/postmaster -i -D 【path】 

数据库备份：  
pg_dump dbname | gzip > filename.gz

创建并还原数据库:

创建数据库:  
createdb -E utf-8 dbname  
gunzip -c filename.gz | psql dbname

 

good lucky

 [1]: http://www.80aj.com/wp-content/uploads/2009/12/pg.jpg