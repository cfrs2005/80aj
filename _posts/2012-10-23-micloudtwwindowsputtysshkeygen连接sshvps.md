---
title: 121023 micloud.tw windows PuTTY SSH KeyGen 连接ssh vps
layout: post
permalink: /2352.html
categories:
  - Linux
tags:
  - micloud.tw windows
  - PuTTY
  - PuTTY下载
  - SSH KeyGen
  - 连接ssh
---
上一章 给大家带来了 台湾免费 vps ，现在是后续各系统版本连接 vps micloud windows 连接ssh: 开始之前 请先下载 PuTTY 下载地址:http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html Windows主机(使用Putty工具连线范例)# 由于Putty采用特有格式的puk档案来封装SSH Key，因此必须透过Putty相关工具将MiCloud产出之Key File进行转换，转换动作如下： (1)打开你得邮件 在邮件中会有私钥的下载，下载至您的电脑中，如下图。 (2)于下列网址下载PuTTy、Pageant and PuTTYgen，该工具可以协助您进行SSH Key的建立与SSH的连线。 网址为:http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html (3)执行puttygen.exe 并点选Load，”档案类型”选择所有档案，导入您所下载的key (4)导入后会才会产生putty可执行的key，并将此金钥储 存，即可关闭程式。 (5)开启pageant.exe执行后程式会在萤幕的右下角如下图: 点开后按下Add key按钮，将上面所储存的key开启。 (6)新增完后请先登入平台选择主机，检视主机的细项画面，再开启putty.exe，hostname为DNS，设定完按下open按钮，进入putty后输入root即可使用。