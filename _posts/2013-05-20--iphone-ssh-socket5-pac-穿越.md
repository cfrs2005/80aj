---
title: 130520 iphone ssh socket5 pac 穿越
layout: post
permalink: /2599.html
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
views:
  - 821
post_views_count:
  - 0
duoshuo_thread_id:
  - 1280248249638191384
categories:
  - Linux
tags:
  - Mac
  - pac协议
  - socket5
  - ssh
---
相比 iphone ssh tunnel 穿越 这次看到的方法远比这个方便得多得多 当然也有一定的特殊性

很古老的方式 iphone自建 sshd 访问时通过 自建机制 穿越：  
内源来自转载未亲测 比较懒

`<br />
准备:</p>
<p>1/ 已破解的iPad, iPhone或 iPod Touch；<br />
2/ 任何一个SSH的客户端软件，比如 iSSH,pTerm,TouchTerm或者Mobile Terminal;<br />
3/ Backgrounder,从Cydia里面安装；<br />
4/ 3proxy, 从Cydia里面安装；</p>
<p>基本概念是:</p>
<p>1/ 用SSH客户端连接到网络上的SSH Tunnel账号(我用的是free-ssh.com的),生成本地SOCKS5 PROXY服务；<br />
2/ 用3Proxy将SOCKS5 proxy 转换成本地的 HTTP Proxy;<br />
3/ 在iPad, iPhone的网络设置里使用本地的 HTTP PROXY；</p>
<p>详细步骤：</p>
<p>1/ 访问 http://www.free-ssh.com , 得到最新的免费 SSH账号的密码;</p>
<p>2/ 运行SSH客户端，键入如下命令，然后敲入最新的密码,用 Backgrounder将其背景运行;</p>
<p>   ssh -p 443 -D 1081 -N free@free-ssh.com</p>
<p>   此时 SOCK5 Proxy已经在背景运行。但是Safari不能直接用SOCKS5Da1L1，所以必须转换成HTTP的Da1L1;</p>
<p>3/ 给3Proxy正确的设置配置文件 /etc/3proxy.cfg, 运行安装的 3proxy，让其背景运行；</p>
<p>   #!/usr/bin/3proxy<br />
   daemon<br />
   auth iponly<br />
   log /var/log/3proxy.log D<br />
   rotate 5<br />
   fakeresolve<br />
   internal 127.0.0.1<br />
   allow * * 127.0.0.1<br />
   parent 1000 socks5+ 127.0.0.1 1081<br />
   proxy -p10180 -a -i127.0.0.1</p>
<p>4/ 最后一步，在ipad,iPhone, iPod Touch里面允许HTTP PROXY,设成：</p>
<p>   HTTP Proxy Server: 127.0.0.1<br />
   HTTP Proxy Port:  1080<br />
`

本文要讲述新的方式

### 流程：

1. 同局域网 pc电脑 通过 ssh Tunnel 自建 socket5 通道  
2. iphone设备链接网络 在 wifi选择的时候 http代理选择 手动 添加url

[<img src="http://pic.80aj.com/2013/05/peizhi-300x225.png" alt="peizhi" width="300" height="225" class="aligncenter size-medium<br />
wp-image-2600" />][1]

http://fengli.me/auto.pac?server=192.168.0.1&#038;port=8080

server 为你的 pc ip  
port 为你的 socket5 端口  
3. 访问 ip.cn 即可看到ip已经更改

 [1]: http://pic.80aj.com/2013/05/peizhi.png