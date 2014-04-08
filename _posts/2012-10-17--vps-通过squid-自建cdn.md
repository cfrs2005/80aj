---
title: 121017 vps 通过squid 自建cdn
layout: post
permalink: /2338.html
bot_views:
  - 5
views:
  - 968
post_views_count:
  - 0
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
duoshuo_thread_id:
  - 1280248249638191321
categories:
  - Linux
tags:
  - cdn
  - squid
  - vps
  - 自建
---
案例：  
Web服务器：域名www.abc.com IP：192.168.21.129 电信单线路接入  
访问用户：电信宽带用户、移动宽带用户  
出现问题：电信用户打开www.abc.com正常，移动用户打开www.abc.com很慢，甚至打不开  
解决方案：在移动机房放置一台CDN代理服务器，通过智能DNS解析，让电信用户直接访问Web服务器、让移动用户访问CDN代理服务器，解决移动用户访问Web服务器慢的问题  
具体操作：  
CDN代理服务器：  
系统：CentOS 5.5 主机名：cdn.abc.com IP:192.168.21.160 安装Squid软件，配置反向代理搭建CDN缓存服务器  
安装前准备：  
1、关闭SELinux

<pre lang="php">vi /etc/selinux/config
   #SELINUX=enforcing     #注释掉
   #SELINUXTYPE=targeted  #注释掉
   SELINUX=disabled  #增加
   :wq  保存，关闭。
   shutdown -r now重启系统
</pre>

2、开启防火墙80端口（后面配置squid的端口为80）

<pre lang="php">vi /etc/sysconfig/iptables
   添加下面的内容
   -A RH-Firewall-1-INPUT -m state –state NEW -m tcp -p tcp –dport 80 -j ACCEPT
   /etc/init.d/iptables restart  #重启防火墙使配置生效
</pre>

3、修改主机的路由模式

<pre lang="php">vi /etc/sysctl.conf
   net.ipv4.ip_forward = 1    #0为关闭，1为开启路由 使用sysctl -p 命令查看
4、修改主机hosts文件，增加域名解析记录
<pre lang="php">
   vi /etc/hosts
   192.168.21.129  www.abc.com    #添加解析记录
</pre>


<p>
  ===========================================================================<br />
  安装开始<br />
  1、安装Squid
</p>


<pre lang="php">
   yum install squid   #安装(Squid 2.6)
   service squid start #启动
   service squid restart #重启
   chkconfig squid on  #设置开机启动
</pre>


<p>
  2、配置Squid  
</p>


<pre lang="php">
  cp /etc/squid/squid.conf /etc/squid/squid.confbak  #备份
  vi  /etc/squid/squid.conf  #编辑文件
 
  http_port 80 transparent  #设置squid端口，默认为3128，设置为80，客户端打开网站的时候不需要输入端口号
  cache_mem 1024 MB   #分配内存大小
  cache_dir ufs /var/spool/squid 4096 16 256 #设置缓存文件大小
  cache_effective_user squid  #设置用户
  cache_effective_group squid  #设置用户组
  access_log /var/log/squid/access.log   #设置访问日志文件
  cache_log /var/log/squid/cache.log  #设置缓存日志文件
  cache_store_log /var/log/squid/store.log  #设置缓存记录文件
  visible_hostname cdn.abc.com  #设置squid服务器主机名
  cache_mgr root@abc.com  #设置管理员邮箱（设置为自己的邮箱地址）
  acl all src 0.0.0.0/0.0.0.0  #设置访问控制列表，默认开启
  http_access allow all  #设置访问权限，默认注释掉的
  cache_peer 192.168.21.129 parent 80 0 no-query originserver name=web  #用户访问web时，Squid向192.168.21.129的80端口发送请求
  cache_peer_domain web www.abc.com  #设置web域名为www.abc.com
  cache_peer_access web allow all  #设置访问权限，允许所有外部客户端访问web
 
  :wq!  #保存退出 
  service squid stop  #停止
  /usr/sbin/squid  -z  #初始化cache缓存目录
  service squid start #启动
</pre>