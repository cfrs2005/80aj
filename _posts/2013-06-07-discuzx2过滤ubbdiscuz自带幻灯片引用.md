---
title: '130607 discuz X2  过滤UBB,discuz自带幻灯片引用'
layout: post
permalink: /2605.html
categories:
  - Code
tags:
  - discuz
  - ubb过滤
  - 代码
  - 幻灯片
---
ubb代码有的时候 dz 数据库直接存了 导致调用的时候看着挺恶心的 这里给个 过滤的 其实是discuz自带的不过被我稍微删了点东西。 discuzUbb代码过滤 function \_ubb\_fillter($string){ $string = preg\_replace( array('/&(#\d{3,5};)/', "/\[hide=?\d\*\](.\*?)\[\/hide\]/is", "/\[\/?\w+=?.\*?\]/"), array('&\\1','<b>\*\*\\*\* Hidden Message \*\*\***</b>',''), $string); return $string; } 论坛改版 需要自己弄个 图片滚动 。jqeury 插件得不兼容一直都认为是 $的问题 这次又遇到了更诡异的事 好吧可能有冲突。 不管怎么样 discuz 自带的还是很简单的 discuz自带幻灯片代码: <div class="slidebox"> <ul class="slideshow"> <!--{loop $bigpic $key $val}--> <li style="width: 345px; height: 293px;"> <a href="{$val[weburl]}" target="\_blank"> <img src="{$val['attachment']}" width="345px;" height="293px;" /> </a> <span class="title">{$val[title]}</span> </li> <!--{/loop}--> </ul> </div> <script lang="javascript"> runslideshow(); </script>