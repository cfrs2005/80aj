---
title: 100714 phpmailer
layout: post
permalink: /1346.html
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