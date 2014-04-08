---
title: 121023 micloud.tw windows PuTTY SSH KeyGen 连接ssh vps
layout: post
permalink: /2352.html
views:
  - 438
duoshuo_thread_id:
  - 1280248249638191325
ta-thumbnail:
  - http://www.80aj.com/wp-content/uploads/2012/10/key.png;http://www.80aj.com/wp-content/uploads/2012/10/putty_download_page.png;http://www.80aj.com/wp-content/uploads/2012/10/load.jpg;http://www.80aj.com/wp-content/uploads/2012/10/file.jpg;http://www.80aj.com/wp-content/uploads/2012/10/sa1.jpg;http://www.80aj.com/wp-content/uploads/2012/10/sa2.jpg;http://www.80aj.com/wp-content/uploads/2012/10/pageant.jpg;http://www.80aj.com/wp-content/uploads/2012/10/sa3.jpg;http://www.80aj.com/wp-content/uploads/2012/10/addkey2.jpg;http://www.80aj.com/wp-content/uploads/2012/10/z1.jpg;
categories:
  - Linux
tags:
  - micloud.tw windows
  - PuTTY
  - PuTTY下载
  - SSH KeyGen
  - 连接ssh
---
上一章 给大家带来了 <a title="台湾免费vps" href="http://www.80aj.com/2348.html" target="_blank">台湾免费 vps</a> ，现在是后续各系统版本连接 vps

micloud windows 连接ssh:

开始之前 请先下载 PuTTY

下载地址:http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html

Windows主机(使用Putty工具连线范例)#

由于Putty采用特有格式的puk档案来封装SSH Key，因此必须透过Putty相关工具将MiCloud产出之Key File进行转换，转换动作如下：  
(1)打开你得邮件 在邮件中会有私钥的下载，下载至您的电脑中，如下图。  
[<img title="key" src="http://www.80aj.com/wp-content/uploads/2012/10/key.png" alt="" width="684" height="512" />][1]

(2)于下列网址下载PuTTy、Pageant and PuTTYgen，该工具可以协助您进行SSH Key的建立与SSH的连线。  
网址为:http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html  
[<img title="putty_download_page" src="http://www.80aj.com/wp-content/uploads/2012/10/putty_download_page.png" alt="" width="865" height="479" />][2]

(3)执行puttygen.exe[  
][2]并点选Load，”档案类型”选择所有档案，导入您所下载的key

[<img title="load" src="http://www.80aj.com/wp-content/uploads/2012/10/load.jpg" alt="" width="483" height="471" />][3]

[<img title="file" src="http://www.80aj.com/wp-content/uploads/2012/10/file.jpg" alt="" width="563" height="387" />][4]

(4)导入后会才会产生putty可执行的key，并将此金钥储[  
][5]存，即可关闭程式。  
[<img title="sa1" src="http://www.80aj.com/wp-content/uploads/2012/10/sa1.jpg" alt="" width="483" height="471" />][6]

[<img title="sa2" src="http://www.80aj.com/wp-content/uploads/2012/10/sa2.jpg" alt="" width="482" height="462" />][7]

(5)开启pageant.exe执行后程式会在萤幕的右下角如下图:

[<img title="pageant" src="http://www.80aj.com/wp-content/uploads/2012/10/pageant.jpg" alt="" width="514" height="252" />][8]

点开后按下Add key按钮，将上面所储存的key开启。

[<img title="sa3" src="http://www.80aj.com/wp-content/uploads/2012/10/sa3.jpg" alt="" width="501" height="357" />][9][  
][10]

[<img title="addkey2" src="http://www.80aj.com/wp-content/uploads/2012/10/addkey2.jpg" alt="" width="501" height="357" />][11]

(6)新增完后请先登入平台选择主机，检视主机的细项画面，再开启putty.exe，hostname为DNS，设定完按下open按钮，进入putty后输入root即可使用。[  
][1][  
][8][  
][11][<img title="z1" src="http://www.80aj.com/wp-content/uploads/2012/10/z1.jpg" alt="" width="953" height="459" />][10][  
][11][  
][12][<img title="dnsport1" src="http://www.80aj.com/wp-content/uploads/2012/10/dnsport1.jpg" alt="" width="928" height="644" />][5][  
][6][  
][7][  
][9][  
][12]

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

 [1]: http://www.80aj.com/wp-content/uploads/2012/10/key.png
 [2]: http://www.80aj.com/wp-content/uploads/2012/10/putty_download_page.png
 [3]: http://www.80aj.com/wp-content/uploads/2012/10/load.jpg
 [4]: http://www.80aj.com/wp-content/uploads/2012/10/file.jpg
 [5]: http://www.80aj.com/wp-content/uploads/2012/10/dnsport1.jpg
 [6]: http://www.80aj.com/wp-content/uploads/2012/10/sa1.jpg
 [7]: http://www.80aj.com/wp-content/uploads/2012/10/sa2.jpg
 [8]: http://www.80aj.com/wp-content/uploads/2012/10/pageant.jpg
 [9]: http://www.80aj.com/wp-content/uploads/2012/10/sa3.jpg
 [10]: http://www.80aj.com/wp-content/uploads/2012/10/z1.jpg
 [11]: http://www.80aj.com/wp-content/uploads/2012/10/addkey2.jpg
 [12]: http://www.80aj.com/wp-content/uploads/2012/10/p1-7.png