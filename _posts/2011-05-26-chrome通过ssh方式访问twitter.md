---
title: 110526 Chrome通过ssh方式访问twitter
layout: post
permalink: /2129.html
categories:
  - Linux
tags:
  - Chrome
  - 方式访问twitter
  - 自架SSH通道
  - 通过ssh
---
 上一次  free vpn Break through the GFW 提供了 免费的vpn帐号 ,如果纯粹的用vpn 的 全剧代理，20分钟掉一次线 用着肯定很不爽， 现在接着上一次的内容继续深入 Chrome 安装插件  Proxy Switchy 链接ssh 访问墙外站点 使用Chrome 打开    https://chrome.google.com/webstore/detail/caehdcpeofiiigpdhbabniblemipncjj 安装 Proxy Switchy 以后,   按照截图设置 内容 保存 &nbsp; Proxy Profiles标签页： 1）Profile Name 随便输入一个名字即可，比如SSH。 2）选择Manual Configuration 3）Socks Proxy：127.0.0.1, Port: 7070（即 前面Myentunnel设置的本地端口），在下面选上Socks V5 点击“Save”按钮保存。 切换到Switch Rules标签页： 1）勾选： Enable Switch Rules 2）勾选： Online Rule List Rule List URL填入：http://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt （被墙列表） Reload Every选择：12 Hours Proxy Profile选择： SSH（与上面的Profile Name保持一致） 3）勾选：AutoProxy Compatible List 点击“Save”按钮保存。 4) 选择Auto Switch Mode 本地架设SSH通道  MyEntunnel 设置如下图 设置完以后 即可访问 www.twitter.com 等一些 gfw 之外的东西了 Proxy Swichy下载: http://u.115.com/file/bhb1kgdz MyEntunnel下载: ﻿ http://u.115.com/file/e60capga#