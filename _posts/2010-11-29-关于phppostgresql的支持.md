---
title: 101129 关于php postgresql的支持
layout: post
permalink: /1580.html
categories:
  - Code
tags:
  - 'Fatal error: Call to undefined function: pg_connect()'
  - php短标签
  - postgresql函数支持
---
 最近遇到2个问题在这里总结下: 1: Fatal error: Call to undefined function: pg\_connect() postgresql windows 已经将php文件中的 extension=php\_pgsql.dll注释去掉,依然报错 至于原因就是没有加载成功 支持postgresql sql的 dll库.如何解决呢？ 安装完postgresql 服务端与客户端以后 在postgresql中的bin目录下 有如下这些dll,拷贝到windows\system32下即可 comerr32.dll gssapi32.dll k5sprt32.dll krb5\_32.dll libeay32.dll libiconv2.dll libintl3.dll libpq.dll ssleay32.dll 2: php 页面执行 直接显示 php代码！ 这样的问题很奇怪,折腾了半天一直以为是php版本导致的,可同样的配置以后还是无法正常解析php,通读报错的地方才发现引用的文件里面的开头竟然是没有php标注的 <?php?>&#8212;-正常的 <??> &#8212;短标签写法 实际上是php.ini的配置没配好导致的  将配置中的  short\_open_tag 设置为on 就可以了