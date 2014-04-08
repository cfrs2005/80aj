---
title: 100126 jquery 之 ajax+json+php 数据刷新
layout: post
permalink: /849.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292289715";s:13:"related_posts";s:1970:"<ul class="related_post"><li><a href="http://blog.80aj.com/2010/12/04/101204-phpase-%e5%8a%a0%e5%af%86/" title="101204 phpase 加密">101204 phpase 加密</a></li><li><a href="http://blog.80aj.com/2010/10/30/101030-%e6%96%87%e4%bb%b6%e6%8a%93%e5%8f%96-snoopy%e7%b1%bb%e4%bb%8b%e7%bb%8d/" title="101030 文件抓取 snoopy类介绍">101030 文件抓取 snoopy类介绍</a></li><li><a href="http://blog.80aj.com/2010/10/29/101029-php-%e4%ba%a7%e5%93%81%e5%ae%89%e8%a3%85%e7%a8%8b%e5%ba%8f%e5%88%b6%e4%bd%9c%e4%bb%a3%e7%a0%81demo/" title="101029 php 产品安装程序制作代码demo">101029 php 产品安装程序制作代码demo</a></li><li><a href="http://blog.80aj.com/2010/10/28/101028-php%e9%a1%b5%e9%9d%a2%e6%89%a7%e8%a1%8c%e6%97%b6%e9%97%b4class/" title="101028 php页面执行时间class">101028 php页面执行时间class</a></li><li><a href="http://blog.80aj.com/2010/09/13/100913-php%e6%8b%9b%e8%81%98%e5%b9%bf%e5%91%8a%e4%b8%80%e5%88%99/" title="100913 PHP招聘广告一则">100913 PHP招聘广告一则</a></li><li><a href="http://blog.80aj.com/2010/08/30/100830-2%e6%ac%be%e6%97%a5%e5%8e%86%e9%80%89%e6%8b%a9%e5%99%a8/" title="100830 2款日历选择器">100830 2款日历选择器</a></li><li><a href="http://blog.80aj.com/2010/08/22/100822-php-%e4%b9%a6%e7%b1%8d%e5%88%86%e4%ba%ab/" title="100822 php 书籍分享">100822 php 书籍分享</a></li><li><a href="http://blog.80aj.com/2010/08/21/100821-php%e4%b9%8b%e8%85%be%e8%ae%af%e5%be%ae%e5%8d%9a-api-%e4%bf%ae%e6%94%b9%e7%89%88/" title="100821 php之腾讯微博 Api 修改版">100821 php之腾讯微博 Api 修改版</a></li><li><a href="http://blog.80aj.com/2010/08/18/100818-%e5%85%b3%e4%ba%8ephp-%e9%9d%a2%e8%af%95/" title="100818 关于php 面试">100818 关于php 面试</a></li><li><a href="http://blog.80aj.com/2010/08/09/100809-php-%e7%ac%a6%e5%8f%b7%e6%b3%a8%e8%a7%a3-%e5%a4%a7%e5%85%a8/" title="100809 php 符号注解 大全">100809 php 符号注解 大全</a></li></ul>";}'
bot_views:
  - 158
duoshuo_thread_id:
  - 1280248249638191147
views:
  - 2
categories:
  - Code
tags:
  - ajax
  - jquery
  - json
  - PHP
  - 定时执行
---
[<img class="aligncenter size-full wp-image-850" title="logo_jquery" src="http://www.80aj.com/wp-content/uploads/2010/01/logo_jquery.gif" alt="" width="230" height="70" />][1]

Jquery 代码

> //创建 ajax 函数  
> function showDate(){  
> //jquery ajax 对象引用  
> $.ajax({
> 
> //传输方式  
> type: &#8220;POST&#8221;,
> 
> //地址 [添加js 以后 可以解决部分 ajax 跨域问题]  
> url: &#8220;[http://222.215.136.13/fortw001/db\_crond/cache/user\_marrylog.js][2]&#8220;,  
> //可加参数  
> data: &#8220;&#8221;,  
> //返回数据类型  
> dataType: &#8220;json&#8221;,  
> //超时时间  
> timeout: 5000,  
> //错误调用函数  
> error:function(){  
> alert(&#8220;查询超时！&#8221;);  
> },  
> //成功调用函数  msg 是个 json 数组 通过定义 返回数据类型 能直接获得一个 js 对象 通过循环 取出数据  
> success: function(msg){  
> var len = msg.length;  
> var htmlval=&#8221;";
> 
> for(var j=0;j<len;j++){
> 
> htmlval += &#8220;<font color=&#8217;#66FF00&#8242;><strong>&#8221;+msg[j].username+&#8221;(&#8220;+msg[j].nuserid+&#8221;)</strong></font>和<font color=&#8217;#66FF00&#8242;><strong>&#8221;+msg[j].benusername+&#8221;(&#8220;+msg[j].benuserid+&#8221;)</strong></font>于&#8221;+msg[j].time+&#8221;喜结连理，恭喜!恭喜!<br>&#8221;;
> 
> }  
> //获取id 为p 的 文档对象  插入 html  
> $(&#8220;#p&#8221;).html(htmlval);
> 
> }  
> });
> 
> }
> 
> // html加载文成以后 调用一个定时执行功能   重复执行
> 
> $(&#8220;document&#8221;).ready(function(){  
> setInterval(showDate,1000);  
> });

PHP 代码

> $arr[]=array(&#8220;nuserid&#8221;=>&#8221;4003&#8243;,&#8221;username&#8221;=>&#8221;白痴&#8221;,&#8221;benuserid&#8221;=>&#8221;411003&#8243;,&#8221;benusername&#8221;=>&#8221;白痴白痴2&#8243;,&#8221;time&#8221;=>&#8217;2010-01-23&#8242;);  
> $arr[]=array(&#8220;nuserid&#8221;=>&#8221;4003&#8243;,&#8221;username&#8221;=>&#8221;白痴&#8221;,&#8221;benuserid&#8221;=>&#8221;411003&#8243;,&#8221;benusername&#8221;=>&#8221;白痴白痴2&#8243;,&#8221;time&#8221;=>&#8217;2010-01-23&#8242;);  
> $arr[]=array(&#8220;nuserid&#8221;=>&#8221;4003&#8243;,&#8221;username&#8221;=>&#8221;白痴&#8221;,&#8221;benuserid&#8221;=>&#8221;411003&#8243;,&#8221;benusername&#8221;=>&#8221;白痴白痴2&#8243;,&#8221;time&#8221;=>&#8217;2010-01-23&#8242;);  
> echo json_encode($arr);

最终生成的json数组:

> [{"nuserid":"4003","username":"\u767d\u75f4","benuserid":"411003","benusername":"\u767d\u75f4\u767d\u75f42","time":"2010-01-23"},{"nuserid":"4003","username":"\u767d\u75f4","benuserid":"411003","benusername":"\u767d\u75f4\u767d\u75f42","time":"2010-01-23"},{"nuserid":"4003","username":"\u767d\u75f4","benuserid":"411003","benusername":"\u767d\u75f4\u767d\u75f42","time":"2010-01-23"}]

 [1]: http://www.80aj.com/wp-content/uploads/2010/01/logo_jquery.gif
 [2]: http://222.215.136.13/fortw001/db_crond/cache/user_marrylog.js