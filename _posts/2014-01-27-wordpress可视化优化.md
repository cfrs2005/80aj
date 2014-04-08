---
title: 140127 wordpress可视化优化
layout: post
permalink: /2729.html
categories:
  - Code
tags:
  - wordpress
  - wp_deregister_script
  - 优化
---
优化是基于lnmp架构的系统，用户访问前端访问加速的优化。并不适合所有用户。 wordpress主题优化 取消头部内容加载 //头部取消wordpress自带jquery加载 //修改当前模板 header.php 在 wp\_head();增加 wp\_deregister\_script("jquery"); //主题function.php里增加下方代码,去掉一些没有必要的内容加载 remove\_action('wp\_head', 'rsd\_link'); remove\_action('wp\_head', 'wlwmanifest\_link'); remove\_action('wp\_head', 'wp\_generator'); wordpress图片优化 LNMP开启对于图片的gzip压缩支持 修改文件 /usr/nginx/conf/nginx.conf增加红色部分 gzip\_types text/plain application/x-javascript text/css application/xml image/jpeg image/gif image/png; 资源图片优化 http://zhanzhang.baidu.com/optimization/index?site=http://www.m2277.com/ wordpress样式优化 利用PHP &#8211; Minify优化css,js进行请求压缩。 下载minify包 http://pan.baidu.com/s/1bn6BLIf //将解压缩后的包min放入主题目录下，注意：当前wordpress需要开启urlwrite //具体引用CSS放头部 header.php <link rel="stylesheet" href="<?php bloginfo('template\_url');?>/min/?b=<?php echo str\_replace(get\_bloginfo('home') . '/', '', get\_bloginfo('template\_directory')); ?>/assets&f=reset.css,mangguo.css"> //具体引用JS放底部 footer.php <script charset="utf-8" src="<?php bloginfo('template\_url');?>/min/?b=<?php echo str\_replace(get\_bloginfo('home') . '/', '', get\_bloginfo('template\_directory')); ?>/assets&f=jquery.min.js,jquery.cookie.js,mangguo.js"></script> wordpress插件缓存优化 后台安装 wp-super-cache，开启预加载。会有点击数不增加BUG，不过这个不是很关注。我们都会用百度,cnnz之类的统计代码。 关于: memcached,redis,Varnish等等是能给wordpress减少大量的db请求,但本质上没有解决用户秒开的问题，所以我没有使用。 非本主题相关 //修改wp-config.php,取消后台编辑文章的修订功能 define('WP\_POST_REVISIONS', false);