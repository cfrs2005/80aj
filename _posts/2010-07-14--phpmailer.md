---
title: 100714 phpmailer
layout: post
permalink: /1346.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292272286";s:13:"related_posts";s:2000:"<ul class="related_post"><li><a href="http://blog.80aj.com/2010/12/04/101204-phpase-%e5%8a%a0%e5%af%86/" title="101204 phpase 加密">101204 phpase 加密</a></li><li><a href="http://blog.80aj.com/2010/10/30/101030-%e6%96%87%e4%bb%b6%e6%8a%93%e5%8f%96-snoopy%e7%b1%bb%e4%bb%8b%e7%bb%8d/" title="101030 文件抓取 snoopy类介绍">101030 文件抓取 snoopy类介绍</a></li><li><a href="http://blog.80aj.com/2010/10/29/101029-php-%e4%ba%a7%e5%93%81%e5%ae%89%e8%a3%85%e7%a8%8b%e5%ba%8f%e5%88%b6%e4%bd%9c%e4%bb%a3%e7%a0%81demo/" title="101029 php 产品安装程序制作代码demo">101029 php 产品安装程序制作代码demo</a></li><li><a href="http://blog.80aj.com/2010/10/28/101028-php%e9%a1%b5%e9%9d%a2%e6%89%a7%e8%a1%8c%e6%97%b6%e9%97%b4class/" title="101028 php页面执行时间class">101028 php页面执行时间class</a></li><li><a href="http://blog.80aj.com/2010/09/13/100913-php%e6%8b%9b%e8%81%98%e5%b9%bf%e5%91%8a%e4%b8%80%e5%88%99/" title="100913 PHP招聘广告一则">100913 PHP招聘广告一则</a></li><li><a href="http://blog.80aj.com/2010/08/22/100822-php-%e4%b9%a6%e7%b1%8d%e5%88%86%e4%ba%ab/" title="100822 php 书籍分享">100822 php 书籍分享</a></li><li><a href="http://blog.80aj.com/2010/08/21/100821-php%e4%b9%8b%e8%85%be%e8%ae%af%e5%be%ae%e5%8d%9a-api-%e4%bf%ae%e6%94%b9%e7%89%88/" title="100821 php之腾讯微博 Api 修改版">100821 php之腾讯微博 Api 修改版</a></li><li><a href="http://blog.80aj.com/2010/08/18/100818-%e5%85%b3%e4%ba%8ephp-%e9%9d%a2%e8%af%95/" title="100818 关于php 面试">100818 关于php 面试</a></li><li><a href="http://blog.80aj.com/2010/08/09/100809-php-%e7%ac%a6%e5%8f%b7%e6%b3%a8%e8%a7%a3-%e5%a4%a7%e5%85%a8/" title="100809 php 符号注解 大全">100809 php 符号注解 大全</a></li><li><a href="http://blog.80aj.com/2010/08/06/100806-%e4%bd%bf%e7%94%a8php%e5%8f%91%e5%a4%a7%e5%9e%8bweb%e7%b3%bb%e7%bb%9f/" title="100806 使用php发大型WEB系统">100806 使用php发大型WEB系统</a></li></ul>";}'
bot_views:
  - 70
duoshuo_thread_id:
  - 1280248249638191217
views:
  - 5
categories:
  - Code
tags:
  - mail
  - PHP
  - php+sendmail+linux
  - phpmailer
  - 标题乱码
  - 正文乱码
---
[<img class="aligncenter size-medium wp-image-1347" title="mail" src="http://www.80aj.com/wp-content/uploads/2010/07/mail-300x207.jpg" alt="" width="300" height="207" />][1]

公司要求sns系统上加个mail插件,在注册以后和找回密码的时候  给用户发送邮件 ，发送注册信息，以及找回密码通道，留住用户。

环境:

php 5.0  +linux+sendmail

查看 sendmail 运行状态linux命令:

<div id="_mcePaste">
  /etc/rc.d/init.d/sendmail status
</div>

<div>
  具体安装可以网上找下：）  windows  的话 推荐用 apmserv 张宴写的
</div>

<div>
  具体调用代码如下：
</div>

> <div>
>   <div>
>     require_once &#8216;class.phpmailer.php&#8217;;
>   </div>
>   
>   <div>
>     $mail = new PHPMailer(); //建立邮件发送类
>   </div>
>   
>   <div>
>     //$mail->CharSet = &#8220;utf-8&#8243;; // 设置编码
>   </div>
>   
>   <div>
>     //$mail->Encoding = &#8220;base64&#8243;; //设置文本编码方式
>   </div>
>   
>   <div>
>     $address = &#8220;****@qq.com&#8221;;//发送邮件地址
>   </div>
>   
>   <div>
>     $mail->IsSMTP(); // 使用SMTP方式发送
>   </div>
>   
>   <div>
>     $mail->Host = &#8220;smtp.****&#8221;; // 您的企业邮局域名
>   </div>
>   
>   <div>
>     $mail->SMTPAuth = true; // 启用SMTP验证功能
>   </div>
>   
>   <div>
>     $mail->Username = &#8220;****&#8221;; // 邮局用户名(请填写完整的email地址)
>   </div>
>   
>   <div>
>     $mail->Password = &#8220;123456&#8243;; // 邮局密码
>   </div>
>   
>   <div>
>     $mail->From = &#8220;NoReply@****&#8221;; //邮件发送者email地址
>   </div>
>   
>   <div>
>     $mail->FromName = iconv(&#8220;utf-8&#8243;, &#8220;gb2312&#8243;, &#8220;80后程序员博客测试&#8221;);
>   </div>
>   
>   <div>
>     $mail->AddAddress(&#8220;$address&#8221;, &#8220;&#8221;); //收件人地址，可以替换成任何想要接收邮件的email信箱,格式是AddAddress(&#8220;收件人email&#8221;,&#8221;收件人姓名&#8221;)
>   </div>
>   
>   <div>
>     //$mail->AddReplyTo(&#8220;&#8221;, &#8220;&#8221;);
>   </div>
>   
>   <div>
>     //$mail->AddAttachment(&#8220;/var/tmp/file.tar.gz&#8221;); // 添加附件
>   </div>
>   
>   <div>
>     $mail->IsHTML(true); // set email format to HTML //是否使用HTML格式
>   </div>
>   
>   <div>
>     //$mail->Subject = &#8220;齐秀社区欢迎你&#8221;; //邮件标题
>   </div>
>   
>   <div>
>     $mail->Subject = iconv(&#8220;utf-8&#8243;, &#8220;gb2312&#8243;, &#8220;&#8221;80后程序员博客测试&#8221;);
>   </div>
>   
>   <div>
>     //$mail->Subject = &#8220;=?utf-8?B?&#8221; . base64_encode(&#8220;&#8221;80后程序员博客测试&#8221;) . &#8220;?=&#8221;; //标题
>   </div>
>   
>   <div>
>     $mail->Body = &#8220;Hello,这是&#8221;80后程序员博客测试邮件&#8221;; //邮件内容
>   </div>
>   
>   <div>
>     $mail->AltBody = &#8220;This is the body in plain text for non-HTML mail clients&#8221;; //附加信息，可以省略
>   </div>
>   
>   <div>
>     if (! $mail->Send()) {
>   </div>
>   
>   <div>
>     echo &#8220;邮件发送失败. <p>&#8221;;
>   </div>
>   
>   <div>
>     echo &#8220;错误原因: &#8221; . $mail->ErrorInfo;
>   </div>
>   
>   <div>
>     exit();
>   </div>
>   
>   <div>
>     }
>   </div>
>   
>   <div>
>     echo &#8220;邮件发送成功&#8221;;
>   </div>
> </div>

phpmailer 类下载地址

http://www.dayanmei.com/download.php?filename=phpmailer.zip

 [1]: http://www.80aj.com/wp-content/uploads/2010/07/mail.jpg