---
title: 121026 js url http https 完美验证 加注释
layout: post
permalink: /2372.html
duoshuo_thread_id:
  - 1280248249638191328
views:
  - 1
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
[<img src="http://www.80aj.com/wp-content/uploads/2012/10/js.jpg" alt="" title="js" width="604" height="332" class="aligncenter size-full wp-image-2373" />][1]

<pre lang="js">function IsURL(str_url){
        var strRegex = "^((https|http|ftp|rtsp|mms)?://)"
        + "(([0-9a-z_!~*'().&#038;=+$%-]+: )?[0-9a-z_!~*'().&#038;=+$%-]+@)?" //ftp的user@
        + "(([0-9]{1,3}\.){3}[0-9]{1,3}" // IP形式的URL- 199.194.52.184
        + "|" // 允许IP和DOMAIN（域名）
        + "([0-9a-z_!~*'()-]+\.)*" // 域名- www.
        + "([0-9a-z][0-9a-z-]{0,61})?[0-9a-z]\." // 二级域名
        + "[a-z]{2,6})" // first level domain- .com or .museum
        + "(:[0-9]{1,4})?" // 端口- :80
        + "((/?)|" // a slash isn't required if there is no file name
        + "(/[0-9a-z_!~*'().;?:@&#038;=+$,%#-]+)+/?)$";
        var re=new RegExp(strRegex,"i");
		//re.test()
        if (re.test(str_url)){
            return (true);
        }else{
            return (false);
        }
}
IsURL("ftp://WWWDZ.cjd:8080");
</pre>

 [1]: http://www.80aj.com/wp-content/uploads/2012/10/js.jpg