---
title: 110608 apache 错误日志 php 短标记
layout: post
permalink: /2152.html
bot_views:
  - 116
duoshuo_thread_id:
  - 1280248249638191283
views:
  - 0
categories:
  - Code
tags:
  - PHP
  - 'The given path is misformatted or contained invalid characters:'
  - 新版本wamp
  - 短标记
---
新版本的 wamp ，短标记的 参数开关被默认为off了 

错误1:\[error] [client 127.0.0.1\] (20024)The given path is misformatted or contained invalid characters: Cannot map GET

错误2:莫名奇妙的将php源码解析成文本 打印到页面上

可能就是短标记没有打开了，在PHP.INI里打开短标记：short\_open\_tag = On，重启Apache，即可