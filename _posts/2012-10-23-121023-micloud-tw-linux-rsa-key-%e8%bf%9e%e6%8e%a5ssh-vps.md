---
title: 121023 micloud.tw linux rsa-key 连接ssh vps
author: 张 清月
layout: post
permalink: /2350.html
duoshuo_thread_id:
  - 1280248249638191324
views:
  - 1
categories:
  - Linux
tags:
  - LINUX
  - micloud.tw
  - rsa-key
  - 连接ssh
---
上一章 给大家带来了 <a href="http://www.80aj.com/2348.html" title="台湾免费vps" target="_blank">台湾免费 vps</a> ，现在是后续各系统版本连接 vps

micloud linx 连接ssh:

MiCloud SSH Key 管理功能

MiCloud提供SSH Key的管理模组，您可透过MiCloud Customer Portal(http://micloud.tw)进行SSH Key的上传与管理，透过SSH协定与SSH Key的认证，将可确保您与您伺服器之间的连线安全。  
Linux/Unix Like 系统建立SSH-KEY与使用方法#

产生SSH Key:

<pre>ssh-keygen -t rsa
#产生过程如下：
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): #按Enter继续下一步
/root/.ssh/id_rsa already exists.
Overwrite (yes/no)? yes #如果已经存在会询问是否覆盖
Enter passphrase (empty for no passphrase): #按Enter继续下一步
Enter same passphrase again: #按Enter继续下一步
Your identification has been saved in /root/.ssh/id_rsa. #private key (预设产出路径为$HOME/.ssh)
Your public key has been saved in /root/.ssh/id_rsa.pub. #public key
The key fingerprint is:
ad:a2:53:fc:2c:eb:f1:3a:3d:6b:44:92:29:33:f0:a5 root@XXXXX.local
#确定并复制产出的SSH Key:
cd $HOME/.ssh/ #切换到SSH Key的预设资料匣
cat id_rsa.pub #读取产出的金钥档案
公开金钥产出格式一不同机器略有不同，但大至上类似下面一串文字：
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAsU6C3X3dwtRcpHDGb1nrYOmdWwsLAu1DVtR+UebO53Cr
QWl7j/FKcLQFPRliiIIsR0rmt5+8s3JyIwkpd+2Ci5Szvhs/URpVhtoei4Xn0TMQg/I/8ZnKHxAsZ2tg
r91eLfYSbMGqqkqS371G68HFDqTgjSAOoPUTWms8afMZ67B/Fr3Yrt8egEaSdpTw== root@XXXX
</pre>

复制这段文字贴于网页中的SSH-Key栏位中即可  
下图为Linux参考画面:  
[<img src="http://www.80aj.com/wp-content/uploads/2012/10/linux_key.png" alt="" title="linux_key" width="866" height="375" class="aligncenter size-full wp-image-2351" />][1]  
Linux/Unix Like 系统连线方式#

使用openssh client，请带参数-i来使用刚刚所建的id_rsa这个private ssh key。  
例如：

<pre>ssh -i id_rsa root@211.123.123.31
</pre>

Linux 主机更新SSH Key#

MiCloud Linux主机于开通主机时会将您帐户资料中之SSH Key汇入新开通的Linux主机中，汇入的目录位于：$HOME/.ssh/authorized_keys档案中，此为一次性设定，日后再登录至MiCloud Customer Portal之SSH Key将不会再写入Linux主机中(SmartOS之认证为结合SSH Key Database之认证，因此不在此限制下)。若您需要更新SSH Key，可采下面步骤：  
产生SSH Key:  
请参考：“MiCloud自助服务操作资讯> SSH金钥相关使用教学”中金钥产生部分。  
将Public Key写入Server端$HOME/.ssh/authorized_keys档案中，以断行隔开  
vi $HOME/.ssh/authorized_keys  
增加您产生的public key至该档案中

 [1]: http://www.80aj.com/wp-content/uploads/2012/10/linux_key.png