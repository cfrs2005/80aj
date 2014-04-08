---
title: 100126 jquery 之 ajax+json+php 数据刷新
layout: post
permalink: /849.html
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