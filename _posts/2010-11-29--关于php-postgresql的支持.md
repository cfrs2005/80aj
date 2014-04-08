---
title: 101129 关于php postgresql的支持
layout: post
permalink: /1580.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292264124";s:13:"related_posts";s:54:"<ul class="related_post"><li>No Related Post</li></ul>";}'
bot_views:
  - 90
duoshuo_thread_id:
  - 1280248249638191262
views:
  - 2
categories:
  - Code
tags:
  - 'Fatal error: Call to undefined function: pg_connect()'
  - php短标签
  - postgresql函数支持
---
[<img class="aligncenter size-medium wp-image-1427" title="php" src="http://www.80aj.com/wp-content/uploads/2010/08/php-300x190.jpg" alt="" width="300" height="190" />][1]

最近遇到2个问题在这里总结下:

1: Fatal error: Call to undefined function: pg_connect()

postgresql windows 已经将php文件中的 extension=php_pgsql.dll注释去掉,依然报错

至于原因就是没有加载成功 支持postgresql sql的 dll库.如何解决呢？

安装完postgresql 服务端与客户端以后 在postgresql中的bin目录下 有如下这些dll,拷贝到windows\system32下即可

<div id="_mcePaste">
  comerr32.dll
</div>

<div id="_mcePaste">
  gssapi32.dll
</div>

<div id="_mcePaste">
  k5sprt32.dll
</div>

<div id="_mcePaste">
  krb5_32.dll
</div>

<div id="_mcePaste">
  libeay32.dll
</div>

<div id="_mcePaste">
  libiconv2.dll
</div>

<div id="_mcePaste">
  libintl3.dll
</div>

<div id="_mcePaste">
  libpq.dll
</div>

<div id="_mcePaste">
  ssleay32.dll
</div>

2: php 页面执行 直接显示 php代码！

这样的问题很奇怪,折腾了半天一直以为是php版本导致的,可同样的配置以后还是无法正常解析php,通读报错的地方才发现引用的文件里面的开头竟然是没有php标注的

> <?php?>&#8212;-正常的  
> <??> &#8212;短标签写法

实际上是php.ini的配置没配好导致的  将配置中的  short\_open\_tag 设置为on 就可以了

 [1]: http://www.80aj.com/wp-content/uploads/2010/08/php.jpg