---
title: 110610 HotNews pro2.5 游客访问统计修改
author: 张 清月
layout: post
permalink: /2158.html
bot_views:
  - 115
duoshuo_thread_id:
  - 1280248249638191285
views:
  - 7
categories:
  - Code
tags:
  - exec无法使用
  - HotNews pro2.5
  - 游客访问统计修改
  - 禁用exec
---
在一些虚拟服务器上，一些危险函数是禁止使用的 如 exec system 等等，新版本的 hotNews pro 2.5 就有这样的问题 ，在这里我贴下我改过的代码 ，有问题的可以修改主题代码就可以解决了

hotnews pro2.5 下载

http://zmingcx.com/hotnews-pro-theme-25.html

文件地址:  
wordpress/wp-content/themes/HotNews/include/counter.php

<pre lang="php"><?php
function MyCounter() {
        date_default_timezone_set('PRC');
	$counter_file = "wp-content/themes/count.txt";
	$count = 0;
	if (file_exists ( $counter_file )) {
		$fp = fopen ( $counter_file, "r" );
		$count = ( int ) fgets ( $fp, 11 );
		fclose ( $fp );
 
	}
	$lasttime = filemtime ( $counter_file );
	if ($lasttime) {
		$lastdate = date ("Y-m-d", $lasttime );
		if ($lastdate != date ("Y-m-d", time () )) {
			$count = 1;
		}
	}
	print "<font color=black>$count&lt;/font>";
	$count ++;
 
	$fp = fopen ( $counter_file, "wb" );
	fwrite ( $fp, $count );
	fclose ( $fp );
}
 
echo ("您是今天第 ");
MyCounter ();
echo (" 位访客");
?>
</pre>