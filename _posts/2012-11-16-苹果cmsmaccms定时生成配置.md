---
title: 121116 苹果Cms(maccms) 定时生成 配置
layout: post
permalink: /2383.html
categories:
  - Code
tags:
  - maccms.定时生成
  - PHP
  - 苹果cms
  - 配置文件
  - 配置方法
---
苹果cms 系统本身是提供 定时生成的 ，基于 无 crontab 或者是 windows 得定时执行的 脚本 执行 都是 在用户访问得时候 激活 。 所以你的网站 要被更新也需要有用户访问。 关于如何开启和配置 maccms 定时生成，请参加下面步骤: 一：开启定时任务任务 系统管理->站点设置->基本->定时任务设定： 开启 二：配置定时任务 系统管理->定时任务配置->添加 // 定时生成首页 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_makehtml.php 执行参数: action=index&#038;flag=vod 执行周期: 任意 执行时间: 任意 //定时生成地图 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_makehtml.php 执行参数: action=map&#038;flag=vod 执行周期: 任意 执行时间: 任意 //定时生成当天数据 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_makehtml.php 执行参数: action=viewday&#038;flag=vod 执行周期: 任意 执行时间: 任意 //定时采集哈库资源 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_maccj.php 执行参数: action=cjday&#038;rday=24&#038;xt=1&#038;cjflag=106\_&#038;cjurl=http://hakuzy.com/xml/maxresxml.asp 执行周期: 任意 执行时间: 任意 //定时采集 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_maccj.php 执行参数: action=cjday&#038;rday=24&#038;xt=1&#038;cjflag=106\_&#038;cjurl=http://hakuzy.com/xml/maxresxml.asp 执行周期: 任意 执行时间: 任意 //定时生成所有自定义页面 任务名称：任意 任务描述：任意 任务状态：开启 执行文件: timming\_makehtml.php 执行参数: action=diypageall 执行周期: 任意 执行时间: 任意