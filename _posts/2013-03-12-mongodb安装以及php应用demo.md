---
title: 130312 mongodb 安装以及php应用Demo
layout: post
permalink: /2565.html
categories:
  - DataBase
tags:
  - mongodb安装
  - mongophp扩展
  - mongo常用操作
---
2013最新语言工作技能需求榜中 前5 已经有2个是 nosql ,nosql的趋势 也在各大厂商被迫跟上潮流中 完善了，总得来说每个人都应该了解 甚至学习 使用下。以下文章是一个Mongodb 的 安装使用过程 MongoDb 下载 //下载最新mongodb 当前文章更新最新版本 wget http://fastdl.mongodb.org/linux/mongodb-linux-i686-2.2.3.tgz //解压缩 tar -zxvf mongodb-linux-i686-2.2.3.tgz //重命名 mv mongodb-linux-i686-2.2.3/ mongodb //新建日志 数据存放 日志文件 mkdir log mkdir data touch log/mongodb.log //配置 mongodb vim aj.conf //文件配置 port=10001 dbpath=data/ logpath=log/mongodb.log logappend=true //启动 ./bin/mongod -f aj.conf Php Mongo 扩展安装 //下载安装包 wget https://github.com/mongodb/mongo-php-driver/archive/master.zip //解压缩 编译 安装 unzip master.zip cd mongo-php-driver-master/ phpize ./configure make all //执行完成会告知你扩展安装目录 sudo make install //编辑php配置文件 增加mongo扩展 vim /etc/php.ini extension=/usr/lib64/php/modules/mongo.so MongoDb 常用PHP操作 $mo = new Mongo("mongodb://localhost:10001"); $coll = $mo->db->cb; $a =array('a'=>'b','email'=>'test@qq.com'); $options=array('safe'=>true); $rs=$coll->insert($a,$options); $new\_a = array('$set'=>array('email'=>'test@gmail.com')); $coll->update(array('a'=>'b'),$new\_a); $c\_rs=$coll->find(); var\_dump($c\_rs); echo "\n\r\n\r"; $one\_email=$coll->findOne(array('a'=>'b'),array('email')); var\_dump($one\_email); 更多关于 Mongo PHP代码操作 可参阅: http://www.php.net/manual/zh/mongo.sqltomongo.php