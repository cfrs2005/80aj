---
title: 121115 centos pptpd 可用下载节点 配置文件
layout: post
permalink: /2378.html
categories:
  - Linux
tags:
  - centos
  - pptpd
  - yum
  - 节点
---
好吧 不要说你不知道 pptpd 是什么，请谷歌下. 悲催得 斯巴达勇士体系 导致 国内centos yum 安装 pptpd 是没有资源节点的 需要自己手动添加 . 

如下面代码

<pre lang="shell">Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.bit.edu.cn
 * extras: mirror.bit.edu.cn
 * updates: mirror.bit.edu.cn
Setting up Install Process
No package pptpd available.
Nothing to do

</pre>

如何安装呢？只需要增加新的节点即可 如下操作即可 yum 安装pptdp  
1:增加可用 pptpd 节点

<pre lang="shell">vi /etc/yum.repos.d/Doylenet.repo，添加如下内容
[doylenet] 
name=Doylenet custom repository for CentOS 
baseurl=http://files.doylenet.net/linux/yum/centos/5/i386/doylenet/ 
gpgcheck=1 
gpgkey=http://files.doylenet.net/linux/yum/centos/RPM-GPG-KEY-rdoyle 
enabled=1
</pre>

2，安装即可

<pre lang="shell">yum install ppp
yum install pptpd
</pre>