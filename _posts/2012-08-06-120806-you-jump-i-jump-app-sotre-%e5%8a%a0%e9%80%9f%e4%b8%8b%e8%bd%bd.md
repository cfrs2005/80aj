---
title: 120806 you jump , i jump app sotre 加速下载
author: 张 清月
layout: post
permalink: /2321.html
bot_views:
  - 176
duoshuo_thread_id:
  - 1280248249638191314
views:
  - 7
categories:
  - Life
tags:
  - appstore
  - exec
  - PHP
  - ping
  - 下载
  - 加速
---
[<img class="aligncenter size-full wp-image-2322" title="ping" src="http://www.80aj.com/wp-content/uploads/2012/08/ping.jpg" alt="" width="456" height="296" />][1]

太多可写 ，太多放弃，懒惰是一个人致命弱点，博客不常更新 经常是因为自己的借口 写得不足够的好  或者无事可写。

其实博客 对于每个人的观点来说是不一样的 ，有琐事，有见解，有事业，有SEO，为活而写。

而我的观点可能是  分享自己的生活，分享自己的见解 ，在分享得过程中，与读者 情感，知识的碰撞，有所领悟，或者能结交共同爱好的人 即可.

app sotre 一直是 景德镇下载的 痛点 因为 apple 并没有在 国内部署下载点 最近的 也在 澳门 香港 日本 。亲 这真的很坑爹。

技术人总有技术人解决的方案不是么：

&nbsp;

<pre lang="php"><?php
set_time_limit ( 0 );
$b = ".phobos.apple.com";
ob_end_flush();   //保证在 firefox 下 持续刷新  
for($i = 1; $i < 200; $i ++) {
	$d = "a" . $i . $b;
	echo "<br />ping  begin

<br />";
	echo $d . "<br />";
	exec ( "ping $d", $list );
	echo $list[$i*12-8];  //为毛是$i*12-8呢 因为 cmd 下ping 一次会返回8行数据 我们只需要每次第3-6 数据即可 其他数据可忽略
	flush ();
	sleep(1); 	
}
</pre>

还可以更优化下:

上述代码只是做了很简单的过滤 取了其中一条 实际上可以把ping 默认取的 4条 读出来 放入 函数中取最小ping timeout

最终输出哪个节点的速度最快 ping多少 IP多少

生成 host 列表 才是最终的效果.

 [1]: http://www.80aj.com/wp-content/uploads/2012/08/ping.jpg