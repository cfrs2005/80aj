---
title: 130218 mysql datetime 默认时间是不支持now 可以添加触发器来使用
author: 张 清月
layout: post
permalink: /2559.html
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
views:
  - 1137
duoshuo_thread_id:
  - 1280248249638191365
categories:
  - DataBase
tags:
  - datetime
  - mysql
  - now
  - timestamp
  - 区别
  - 触发器
---
从我接触mysql开始 就一直在关于时间日期上 喜欢用 timestamp 这样的话 默认个 now 就可以了 不需要自己去每次插入的时候 php 进行当前时间查询

公司某项目不知道为什么会选择 innodb 这种2得不能再2的数据库 做 一个普通的社交 网站的数据库原型。

在使用过程中发现 所有的发布时间都为空，查了半天是源自于 dateitime 是设置为空 并且就算你写上now 也是不支持的。

### 关于 datetime , timestamp 的区别 

**相同**

显示

TIMESTAMP列的显示格式与DATETIME列相同。换句话说，显示宽度固定在19字符，并且格式为YYYY-MM-DD HH:MM:SS。

**不同**

范围

datetime 以&#8217;YYYY-MM-DD HH:MM:SS&#8217;格式检索和显示DATETIME值。支持的范围为&#8217;1000-01-01 00:00:00&#8242;到&#8217;9999-12-31 23:59:59&#8242;TIMESTAMP值不能早于1970或晚于2037

储存

TIMESTAMP

1.4个字节储存（Time stamp value is stored in 4 bytes）

2.值以UTC格式保存（ it stores the number of milliseconds）

3.时区转化 ，存储时对当前的时区进行转换，检索时再转换回当前的时区。

datetime

1.8个字节储存（8 bytes storage）

2.实际格式储存（Just stores what you have stored and retrieves the same thing which you have stored.）

3.与时区无关（It has nothing to deal with the TIMEZONE and Conversion.）

### 如何解决 datetime 默认时间设置为now ? 下面提供一个简单的触发器函数

<pre lang="mysql">delimiter //
DROP TRIGGER IF EXISTS default_datetime//
create trigger default_datetime before insert on shai_item
     for each row
     if new.create_time = '0000-00-00 00:00:00' then
       set new.create_time = now();
     end if;//
delimiter ;

</pre>