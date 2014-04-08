---
title: 130416 macos shell 管理众ssh服务器
layout: post
permalink: /2584.html
categories:
  - Linux
tags:
  - macos
  - shell
  - ssh
  - sshpass
  - 服务器管理
---
喵了个咪的 写的文章再次被手指撸了 气氛 文章为记录在 macos 懒人奋斗战报 sshpass : linux 可以直接命令行 连接 带密码的 ssh服务器 格式： sshpass -p password ssh root@hostloc 下载地址: http://sourceforge.net/projects/sshpass/?source=navbar shell 管理服务器脚本 #!/bin/bash function checkim(){ user=\`whoami\` if [ "$user" != "root" ]; then read -p "You Password: " rootpass sudo su - echo $rootpass fi } function alert(){ echo -e "$1" } function add(){ echo "add a server to your local conf" read -p "server name: " sname read -p "server user: " suer read -p "server host: " shost read -p "server pass: " spass echo $sname $suer $shost $spass >> host.cf } function del(){ echo -e "del server" } function goto(){ list read -p "input server name:" h a=\`grep $h host.cf | awk '{print $2}'\` b=\`grep $h host.cf | awk '{print $3}'\` c=\`grep $h host.cf | awk '{print $4}'\` if [ ! -n $c] ;then sshpass -p $c ssh $a@$b else ssh $a@$b fi exit 0 } function list(){ alert "" echo "your owner server list"; awk -F ' ' '{print $1,$2}' host.cf alert "" } function main(){ echo -e "please choose your command for service\n\r" echo -e "1.server list" echo -e "2.server add" echo -e "3.server del" echo -e "4.server goto" echo -e "5.close this shell" } function version(){ echo -e "author : 80aj url: http://www.80aj.com" echo -e "for cmommand manage linux server" } clear version alert " " #checkim while : do main read -p "choose your service:" cmd case "$cmd" in 1) list;; 2) add;; 3) del;; 4) goto;; 5) echo "Bye !";exit 0;; *) echo "input error" esac done exit 0 goodjob bye ~