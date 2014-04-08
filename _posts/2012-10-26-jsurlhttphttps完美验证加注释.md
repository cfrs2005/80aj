---
title: 121026 js url http https 完美验证 加注释
layout: post
permalink: /2372.html
categories:
  - Code
tags:
  - http
  - https
  - JS
  - Url
  - 完美验证
  - 正则
  - 注释版
---
 function IsURL(str\_url){ var strRegex = "^((https|http|ftp|rtsp|mms)?://)" + "((\[0-9a-z\_!~\*'().&#038;=+$%-]+: )?[0-9a-z\_!~\*'().&#038;=+$%-]+@)?" //ftp的user@ + "(([0-9]{1,3}\.){3}[0-9]{1,3}" // IP形式的URL- 199.194.52.184 + "|" // 允许IP和DOMAIN（域名） + "([0-9a-z\_!~\*'()-]+\.)\*" // 域名- www. + "([0-9a-z\]\[0-9a-z-\]{0,61})?[0-9a-z]\." // 二级域名 + "[a-z]{2,6})" // first level domain- .com or .museum + "(:[0-9]{1,4})?" // 端口- :80 + "((/?)|" // a slash isn't required if there is no file name + "(/[0-9a-z\_!~*'().;?:@&#038;=+$,%#-]+)+/?)$"; var re=new RegExp(strRegex,"i"); //re.test() if (re.test(str\_url)){ return (true); }else{ return (false); } } IsURL("ftp://WWWDZ.cjd:8080");