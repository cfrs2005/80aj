---
title: 130217 discuz x feed 添加 Demo演示
layout: post
permalink: /2558.html
categories:
  - Code
tags:
  - discuz
  - feed
  - 添加feed
  - 演示
---
Discuz 在未一些 外部应用增加 feed 的时候 可以直接调用 feed_add 函数 。 

以下是函数原型:

<pre lang="php">feed_add($icon, $title_template='', $title_data=array(), $body_template='', $body_data=array(), $body_general='', $images=array(), $image_links=array(), $target_ids='', $friend='', $appid='', $returnid=0, $id=0, $idtype='', $uid=0, $username='') {
</pre>

使用前需要:

<pre lang="php">require_once libfile('function/feed');
</pre>

**其中$icon是动态的图标，$title\_template是标题部分，$body\_general 是一个双引号的说明，$body_template是中间部分内容，其它参数我没去了解，也用不上。**

以下是例子: 

<pre lang="php">require_once libfile('function/feed');
$icon='starluck';
$title_template=$username."在xxx中对自己使用了xxx. &lt; a href='plugin.php?id=wuxing:starluck'>我也要去看看运气&lt;/a>";

$body_general="幸运一转,运气全名";

feed_add($icon,$title_template,NULL,'这是什么',NULL,$body_general);
</pre>

本文转自 : http://www.2015pc.com/thread-16904-1-1.html