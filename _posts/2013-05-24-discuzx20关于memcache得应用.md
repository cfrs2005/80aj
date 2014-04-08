---
title: 130524 discuz x2.0 关于 memcache得应用
layout: post
permalink: /2603.html
categories:
  - Code
tags:
  - discuz
  - memcache
  - sesion
  - 多组
  - 应用
---
让discuz支持多组memcache discuz 是不支持多组memcache 共同使用 所以我们需要修改代码: //修改公共配置文件 bbs/config/config\_global.php $\_config\['memory'\]\['memcache'\]\['server'] = 'true'; $\_config['memory'\]\['memcache'\]\['host'\]\[\]='192.168.1.1'; $\_config\['memory'\]\['memcache'\]\['host'\]\[\]='192.168.1.2'; //$\_config\['memory'\]\['memcache'\]\['server'] = 'localhost'; //$\_config['memory'\]\['memcache'\]\['port'] = 11211; $\_config['memory'\]\['memcache'\]\['pconnect'] = 1; $\_config['memory'\]\['memcache'\]\['timeout'] = 1; //修改 discuz memcache class类 bbs/source/class/class\_memcache.php function init($config) { if (! empty ( $config ['server'] )) { $this->obj = new Memcache (); if ($config ['pconnect']) { $i = 1; foreach ( $config ['host'] as $one\_host ) { if ($i == 1) { $connect = @$this->obj->pconnect ( $one\_host, 11211 ); } else { $connect = @$this->obj->addServer ( $one\_host, 11211 ); } $i ++; } // $connect = @$this->obj->pconnect($config['server'], $config['port']); //因为使用长连接 短连接就不改了 } else { $connect = @$this->obj->connect ( $config ['server'], $config ['port'] ); } $this->enable = $connect ? true : false; } } discuz memcache 使用 require\_once libfile('class/memcache'); @include DISCUZ\_ROOT.'./config/config\_global.php'; //获取 $m = new discuz\_memcache(); $m->init($\_config['memory'\]\['memcache'\]); $mail="5991168@qc.com"; $userinfo=$m->get(md5($email)); //写入 $md5\_name=md5($email); $m->set($md5\_name,$userinfo,MEMCACHE\_COMPRESSED,time()+43200); discuz 存储session by memcache //修改配置文件 php.ini php\_value[session.save\_handler] = memcached php\_value[session.save\_path] = 192.168.1.1:11211