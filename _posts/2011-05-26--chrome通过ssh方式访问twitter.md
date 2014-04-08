---
title: 110526 Chrome通过ssh方式访问twitter
layout: post
permalink: /2129.html
bot_views:
  - 104
duoshuo_thread_id:
  - 1280248249638191278
views:
  - 0
categories:
  - Linux
tags:
  - Chrome
  - 方式访问twitter
  - 自架SSH通道
  - 通过ssh
---
[][1][][2][][3][  
][4]上一次 <a href="http://www.80aj.com/2011/05/26/110526-free-vpn-break-through-the-gfw/" target="_blank"> free vpn Break through the GFW </a>提供了 免费的vpn帐号 ,如果纯粹的用vpn 的 全剧代理，20分钟掉一次线 用着肯定很不爽， 现在接着上一次的内容继续深入

Chrome 安装插件  Proxy Switchy 链接ssh 访问墙外站点

使用Chrome 打开    <https://chrome.google.com/webstore/detail/caehdcpeofiiigpdhbabniblemipncjj>

安装 Proxy Switchy 以后,   按照截图设置 内容 保存

[][4]

&nbsp;

[<img class="aligncenter size-medium wp-image-2131" style="display: block; margin-left: auto; margin-right: auto; border: 0px initial initial;" title="pr1" src="http://www.80aj.com/wp-content/uploads/2011/05/pr1-300x150.jpg" alt="" width="300" height="150" />][4]

[<img class="aligncenter size-medium wp-image-2132" title="pr2" src="http://www.80aj.com/wp-content/uploads/2011/05/pr2-300x117.jpg" alt="" width="300" height="117" />][1]

[<img class="aligncenter size-full wp-image-2133" title="pr3" src="http://www.80aj.com/wp-content/uploads/2011/05/pr3.jpg" alt="" width="200" height="268" />][2]

<div>
</div>

Proxy Profiles标签页：

1）Profile Name 随便输入一个名字即可，比如SSH。

2）选择Manual Configuration

3）Socks Proxy：127.0.0.1, Port: 7070（即 前面Myentunnel设置的本地端口），在下面选上Socks V5

点击“Save”按钮保存。

切换到Switch Rules标签页：

1）勾选： Enable Switch Rules

2）勾选： Online Rule List

Rule List URL填入：<a title="gfwlist" href="http://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt" target="_blank">http://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt</a> （被墙列表）

Reload Every选择：12 Hours

Proxy Profile选择： SSH（与上面的Profile Name保持一致）

3）勾选：AutoProxy Compatible List

点击“Save”按钮保存。

4) 选择Auto Switch Mode

本地架设SSH通道  MyEntunnel

设置如下图

[<img class="aligncenter size-medium wp-image-2134" title="pr4" src="http://www.80aj.com/wp-content/uploads/2011/05/pr4-300x191.jpg" alt="" width="300" height="191" />][3]

设置完以后 即可访问 [www.twitter.com][5] 等一些 gfw 之外的东西了

Proxy Swichy下载:

<http://u.115.com/file/bhb1kgdz>

MyEntunnel下载:

<div id="_mcePaste" class="mcePaste" style="position: absolute; width: 1px; height: 1px; overflow: hidden; top: 0px; left: -10000px;">
  ﻿
</div>

<http://u.115.com/file/e60capga>#

 [1]: http://www.80aj.com/wp-content/uploads/2011/05/pr2.jpg
 [2]: http://www.80aj.com/wp-content/uploads/2011/05/pr3.jpg
 [3]: http://www.80aj.com/wp-content/uploads/2011/05/pr4.jpg
 [4]: http://www.80aj.com/wp-content/uploads/2011/05/pr1.jpg
 [5]: http://www.twitter.com