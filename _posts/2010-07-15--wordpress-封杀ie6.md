---
title: 100717 wordpress 封杀ie6
layout: post
permalink: /1359.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292244302";s:13:"related_posts";s:54:"<ul class="related_post"><li>No Related Post</li></ul>";}'
bot_views:
  - 159
duoshuo_thread_id:
  - 1280248249638191218
views:
  - 2
categories:
  - Code
tags:
  - ie6nomore
  - ie6封杀
  - js代码
  - 拒绝ie6
---
[<img class="aligncenter size-full wp-image-1360" title="ie6nomore" src="http://www.80aj.com/wp-content/uploads/2010/07/ie6nomore.jpg" alt="" width="637" height="109" />][1]

使用Ie6 访问本博客会出现一些样式错误，导致不美观，虽然我不是一个很追求完美的人，但总不喜欢给访客带来一些 视觉上的不爽快，所以今天在头部添加了  封杀Ie6代码。

关于封杀Ie6的事情:

IE6是一款老土的浏览器，这八年来推出的大多数新功能它都不支持，不过这款浏览器的用户量仍然占15-25%左右，这严重制约了浏览器技术的向前发展。 许多人都认为是时候彻底抛弃这款老土浏览器了，不过现在，有此想法的已经不仅仅是个人和一些非赢利性的组织，有几家公司甚至已经联合推出了一个呼吁人们抛 弃IE6的主题网站“IE6 No More”。

<http://www.ie6nomore.com/>

封杀代码如下:

> <!&#8211;[if lt IE 7]>  <div style=&#8217;border: 1px solid #F7941D; background: #FEEFDA; text-align: center; clear: both; height: 75px; position: relative;&#8217;>    <div style=&#8217;position: absolute; right: 3px; top: 3px; font-family: courier new; font-weight: bold;&#8217;><a href=&#8217;#&#8217; onclick=&#8217;javascript:this.parentNode.parentNode.style.display=&#8221;none&#8221;; return false;&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-cornerx.jpg&#8217; style=&#8217;border: none;&#8217; alt=&#8217;Close this notice&#8217;/></a></div>    <div style=&#8217;width: 640px; margin: 0 auto; text-align: left; padding: 0; overflow: hidden; color: black;&#8217;>      <div style=&#8217;width: 75px; float: left;&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-warning.jpg&#8217; alt=&#8217;Warning!&#8217;/></div>      <div style=&#8217;width: 275px; float: left; font-family: Arial, sans-serif;&#8217;>        <div style=&#8217;font-size: 14px; font-weight: bold; margin-top: 12px;&#8217;>You are using an outdated browser</div>        <div style=&#8217;font-size: 12px; margin-top: 6px; line-height: 12px;&#8217;>For a better experience using this site, please upgrade to a modern web browser.</div>      </div>      <div style=&#8217;width: 75px; float: left;&#8217;><a href=&#8217;http://www.firefox.com&#8217; target=&#8217;\_blank&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-firefox.jpg&#8217; style=&#8217;border: none;&#8217; alt=&#8217;Get Firefox 3.5&#8242;/></a></div>      <div style=&#8217;width: 75px; float: left;&#8217;><a href=&#8217;http://www.browserforthebetter.com/download.html&#8217; target=&#8217;\_blank&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-ie8.jpg&#8217; style=&#8217;border: none;&#8217; alt=&#8217;Get Internet Explorer 8&#8242;/></a></div>      <div style=&#8217;width: 73px; float: left;&#8217;><a href=&#8217;http://www.apple.com/safari/download/&#8217; target=&#8217;\_blank&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-safari.jpg&#8217; style=&#8217;border: none;&#8217; alt=&#8217;Get Safari 4&#8242;/></a></div>      <div style=&#8217;float: left;&#8217;><a href=&#8217;http://www.google.com/chrome&#8217; target=&#8217;\_blank&#8217;><img src=&#8217;http://www.ie6nomore.com/files/theme/ie6nomore-chrome.jpg&#8217; style=&#8217;border: none;&#8217; alt=&#8217;Get Google Chrome&#8217;/></a></div>    </div>  </div>  <![endif]&#8211;>

 [1]: http://www.80aj.com/wp-content/uploads/2010/07/ie6nomore.jpg