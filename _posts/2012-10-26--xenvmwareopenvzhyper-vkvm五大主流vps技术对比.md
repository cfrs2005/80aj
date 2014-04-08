---
title: 121026 XEN,Vmware,OpenVZ,Hyper-V,KVM五大主流vps技术对比
layout: post
permalink: /2369.html
views:
  - 709
duoshuo_thread_id:
  - 1280248249638191326
categories:
  - Linux
tags:
  - Hyper-V
  - KVM
  - OpenVZ
  - Vmware
  - Vps技术
  - XEN
  - 对比
---
[  
<img class="aligncenter" title="linux_vps" src="http://www.80aj.com/wp-content/uploads/2012/10/linux_vps.gif" alt="" width="458" height="289" />][1]

<span style="color: #ff0000;"><strong>XEN</strong> </span>也是著名的开源虚拟化软件。基于半虚拟化技术。一直作为Linux内置的虚拟化技术（在新的Linux发行版已经取消掉。Linux开始支持新的虚拟化技术KVM），有很大的用户群体。他的优点很多，对带宽的细节控制做的非常好，用户体验也很好，重做系统可以让用户直接通过网页进行，国外也有很多基于XEN开发的第三方VPS控制软件。但是他有一个致命的缺点，这个缺点是所有基于Linux为核心的，包括Vmware、OpenVZ都有的一个缺点，磁盘性能差。可能跟Linux下的驱动不完善有关吧。虚拟化技术，就是将日趋发展的CPU资源最大化的利用，但是磁盘性能不行，根本谈不上虚拟化。更别想获得多好的体验了。

**<span style="color: #ff0000;">Vmware</span>**，全球最早涉及到虚拟化的一款软件产品。也是最初很多IDC选用的VPS技术。目前市场中这类VPS较多。Vmware的磁盘I/O性能一直表现不好。另外，CPU性能也比不上Hyper-V。唯一的优势就是对多种操作系统的支持比较好。加上Vmware的元老级的身份，对虚拟化也有着自己独特的思考。

**<span style="color: #ff0000;">OpenVZ</span>**（简称OVZ）采用SWsoft的Virutozzo虚拟化服务器软件产品的内核，是基于Linux平台的操作系统级服务器虚拟化架构。这个架构直接调用母服务器（母机）中的内核，模拟生成出子服务器（VPS，小机），所以，它经过虚拟化后相对于母服务器，性能损失大概只有的1-3%。

**<span style="color: #ff0000;">HyperV</span>**的技术，很多IT媒体网站讨论的比较多，在这里不一一列举。作为一个最终的用户，我们对四种方案都进行了测试。不得不承认，Hyper-V的性能是最好的。原因，首先是，Windows有非常完善的驱动，就I/O磁盘性能来说，Vmware、XEN、Vz等，对RAID5的支持都不是很好，在300G SAS*5的情况下，磁盘读取不超过500M/S，写入不超过350M/S，而在Hyper下面，这两个数字可以达到700M/S和550M/S以上。

**<span style="color: #ff0000;">KVM</span>**的技术,有人说它比xen更好的一点，因为kvm是完全虚拟。 更形象的说，kvm是linux的一部分, 可使用通常的linux调度器和内存管理，并且从qemu继承了丰富的磁盘格式, 所支持的磁盘格式包括裸映象, 原始qemu格式, VMware格式和更多。

### <span style="color: #ff0000;">根据我个人经验来看:</span>

#### 再不超售的情况下 VPS 使用度排名 :

KVM->OpenVZ->XEN ->HyperV->Vmware

#### 超售情况下 VPS 使用度排名 :

KVM->XEN->OpenVZ->HyperV->Vmware

这里介绍得只是技术上面得 如果要选择 Vps 其实 还要看很多方面 在以后得文章里会带来更多。

### <span style="color: #ff0000;">下期预告:</span>

**如何选择一款理想的VPS:**

*   XEN,Vmware,OpenVZ,Hyper-V,KVM五大主流vps技术对比
*   国外VPS线路哪些适合中国地区访问
*   VPS真得只要有了CPU和内存就可以了吗?
*   推介 几款 本人用过得VPS[  
    ][1]

### <span style="color: #ff0000;">讨论:</span>

如果你有什么想法,可以给我留言或者评论 3ks

 [1]: http://www.80aj.com/wp-content/uploads/2012/10/linux_vps.gif