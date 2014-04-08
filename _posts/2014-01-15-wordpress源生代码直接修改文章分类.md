---
title: 140115 wordpress 源生代码直接修改文章分类
layout: post
permalink: /2701.html
categories:
  - Code
tags:
  - wordpress
  - wp_set_post_categories
  - 小说站
  - 文章分类
---
昨天论坛干货看了个关于单本小说论坛的事，本来这事知道很早，也能很好的Seo,做起来也很简单，没想到权重可以这么高，反正不废什么事，于是自己做了个，过程中遇到了 分类转换的问题，当然这里已经解决了，共享下： <?php // wordpress 目录新建个 reset\_cat.php 复制代码 稍作修改即可 // wordpress 源生代码解决批量分类转换 目前用于 小说站的分类解决 // 有问题请联系 cfrs2005(Hostloc@cfrs2005) // 博客:80aj.com // 2014/01/15 include "wp-config.php"; error\_reporting ( E\_ALL ); global $wpdb; //文章序列号 开始到结束 可自行修改代码 $begin\_end\_arr = array ( '6' => array ( 1048, 1400 ) ); foreach ( $begin\_end\_arr as $key => $single\_arr ) { $posts = $wpdb->get\_results ( "SELECT id FROM $wpdb->posts where id >={$single\_arr[0]} and id<={$single\_arr[1]}" ); foreach ( $posts as $post ) { wp\_set\_post\_categories ( $post->id, array ( $key ) ); } } 单站小说: http://www.jueshitangmenquanben.com 绝世唐门全本 By the way: 出售小说站源码采集+自动更新 only for liunx demo: 采集开始 开始处理 总数据 7 条 http://www.xxxx.com/xxx113773.html 当前文章 第三佰四一章 龙皇、饕餮、本体（上） 已经插入过 标题无变更 http://www.xxx.com/xx115793.html 当前文章 第三百四拾一章 龙皇、饕餮、本体（中）下）14第三 已经插入过 标题无变更 http://www.xxx.com/xx119686.html 当前文章 第三百四一章节 龙皇、饕餮、本体（下）第三04 已经插入过 标题无变更 http://www.xxx.com/xx2164.html 当前文章 第三百四二章节 黄金蝶龙变（上）第三04中） 已经插入过 标题无变更 http://www.xxx.com/xx22169.html 当前文章 第三佰四二章 黄金蝶龙变（中） 已经插入过 标题无变更 http://www.xxx.com/xx28248.html 当前文章 第三百四拾二章 黄金蝶龙变（下）中）14第三 已经插入过 标题无变更 http://www.xxx.com/xx1309.html 当前文章 第三百四三章节 好多、好多啊！第三04 已经插入过 标题无变更 执行结束