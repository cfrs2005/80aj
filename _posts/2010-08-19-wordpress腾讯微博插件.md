---
title: 100819 wordpress 腾讯微博插件
layout: post
permalink: /1467.html
categories:
  - Code
tags:
  - wordpress
  - 显示所有内容
  - 腾讯微博插件
  - 部分代码修改
---
<p style="text-align: center;">
  <a href="http://www.80aj.com/wp-content/uploads/2010/08/wb.jpg"><img class="aligncenter size-full wp-image-1468" title="wb" src="http://www.80aj.com/wp-content/uploads/2010/08/wb.jpg" alt="" width="486" height="282" /></a>
</p>

腾讯微博是我一直用的微博，上面一直跟新一些精彩的小段子,很想分享到博客上来,做更多的内容填充,网上搜索了下,找到个不错的插件:

PS:直接调用地址 <http://q.hzlzh.com/keleyan> 返回的是一个josn数组

=== wordpress-tencent-microblog ===  
Contributors: HzlzH  
Donate link: http://www.hzlzh.com/wordpress-tencent-microblog/  
Tags: 腾讯微博,QQ,微博,腾讯,同步  
Requires at least: 2.7  
Tested up to: 3.0.1  
Stable tag: 1.0.5

显示腾讯微博发言的插件，无需密码，安全可靠，采取缓存机制。利用民间API，支持1-10条发言输出。

== Description ==

显示腾讯微博发言的插件，无需密码，即可从 民间API 处获得消息，显示在wordpress侧边栏上，安全可靠。采用了缓存机制，可自定义刷新时间，不占用站点加载速度。可以在[外观]–[小工具]中调用，也可以在任意位置使用&#8220; 调用。

== Installation ==

1. 上传 \`wordpress-tencent-microblog\`插件到 \`/wp-content/plugins/\` 目录  
2. 在Wordpress后台控制面板”插件(Plugins)”菜单下激活”wordpress-tencent-microblog”  
3. 在Wordpress后台控制面板”外观(Appearance)->小工具(Widgets)”下使用\`腾讯微博\`

== Frequently Asked Questions ==

= 我不想在侧边栏调用，而是在任意位置可以么？怎么做？ =

可以！需要激活插件后，在任意位置使用&#8220;调用即可，只需要修改\`you-ID\` 为你的腾讯微博帐号，\`5\`是你想要展示的条数。

目前官方没有开放API，待开放时，我会第一时间更新。

= 有腾讯微博官方的API吗？ =

目前官方没有开放API，待开放时，我会第一时间更新。

= 如果我的HOST不支持copy()函数怎么办？ =

可以去除缓存功能，直接抓取API即可，参见 使用说明

== Screenshots ==

1. 使用侧边栏[小工具]调用的效果  
2. 后台截图

== Changelog ==

= V 1.0.5 =  
*修改了几个重要的注释  
*提供了WIN主机无法使用copy()函数的解决方案注释  
*修改了一些细节

= V 1.0.3 =  
*现在支持 1至10 条的发言调用  
*修复了有实名认证的用户的显示错误BUG  
*加入了 CSS 样式，预留自定义接口

= V 1.0.0 =  
*在Wordpress中同步显示腾讯微博中的发言  
*无需登录，采取民间API，安全可靠  
*由于使用缓存，本插件目录需要有写入权限  
*目前调取显示数量为1条，更多需要API的支持，尽在下一个版本

== Upgrade Notice ==

= V 1.0.5 =  
修改了几个重要的注释，提供了WIN主机无法使用copy()函数的解决方案注释

= 1.0.3 =  
本版本已经完善了10条以内信息的完善，并且预留了CSS样式名

= 1.0.0 =  
这个是第一个版本，由于API限制只能调用1发言

Related posts:

1.  <a title="Permanent Link: 西小西博客首页空白|wordpress blank index page" rel="bookmark" href="http://www.xixiaoxi.com/2009/05/%e8%a5%bf%e5%b0%8f%e8%a5%bf%e5%8d%9a%e5%ae%a2%e9%a6%96%e9%a1%b5%e7%a9%ba%e7%99%bdwordpress-blank-index-page.html">西小西博客首页空白|wordpress blank index page</a>哎~成就感！ 忙活了两个晚上，总算找到了wordpress首页空白的原因。 i have&#8230;
2.  <a title="Permanent Link: 西小西博客创建WAP版" rel="bookmark" href="http://www.xixiaoxi.com/2009/03/blogwap.html">西小西博客创建WAP版</a>西小西的wordpress博客创建WAP版，目的是手机上网，现在手机上网太普遍啦，以后资费还能下调，手机网络时代即将到来。 今天百度google了一番，还是觉得WP-T-WAP插件好用些，推荐大家使用。 下面简单介绍下两个常见插件 一&#8230;
3.  <a title="Permanent Link: WP Mail SMTP|WordPress mail()发送邮件|WordPress mail()函数SMTP" rel="bookmark" href="http://www.xixiaoxi.com/2009/04/wordpress-mail-smtp.html">WP Mail SMTP|WordPress mail()发送邮件|WordPress mail()函数SMTP</a>今天又学习了一招~wordpress利用wp mail smtp 插件发邮件！&#8230;
4.  <a title="Permanent Link: WordPress QQ表情插件Custom Smilies" rel="bookmark" href="http://www.xixiaoxi.com/2009/08/wordpress-qq%e8%a1%a8%e6%83%85%e6%8f%92%e4%bb%b6custom-smilies.html">WordPress QQ表情插件Custom Smilies</a>今天西小西调试好了WordPress表情插件Custom Smilies，而且还把插件原来的图片换成QQ表情，那就叫WordPress QQ表情插件吧~ 第一次见到这个功能是在Willin&#8230;
5.  <a title="Permanent Link: wordpress不用插件实现多语言切换|wordpress language changes without plug-in" rel="bookmark" href="http://www.xixiaoxi.com/2009/03/wordpress-language-changes.html">wordpress不用插件实现多语言切换|wordpress language changes without plug-in</a>以本站西小西|xixiaoxi.com网站切换英文为例。 1. 在边栏添加个文本框，我把切换语言的文本框放在右上角啦，看本站效果。 2&#8230;.

<span style="color: #ff0000;"><strong>由于微博显示有些小缺点稍微更改了下代码，这样当鼠标划上去的时候能看到整个博文,140个字短短的一行是显示不了的,修改代码如下:</strong></span>

> echo &#8216;<li><img style=&#8221;float:left;padding-right:3px;padding-top:10px;&#8221; alt=&#8221;腾讯微博&#8221; src=&#8221;&#8216;.WP\_PLUGIN\_URL.&#8217;/wordpress-tencent-microblog/txwb.gif&#8221; /><a href=&#8221;http://t.qq.com/&#8217;.$username.&#8217;&#8221; rel=&#8221;external nofollow&#8221; title=&#8221;&#8216;.$decodedArray\[contents\]\[$i\]\[content].&#8217;&#8221;>&#8217;.$decodedArray[contents\]\[$i\][content].&#8217;</a></li>&#8217;;