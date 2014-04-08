---
title: 100407 php url_encode 加密解密函数
layout: post
permalink: /1009.html
categories:
  - Code
tags:
  - 80slife
  - PHP
  - url_encode
  - wp Audio Player
  - 加密解密函数
  - 可乐烟
---
 /*\*  \*wp Audio Player 插件音乐地址加密函数  \*@date 2010/04/07  \*代码阅读注释添加:  \* @author :可乐烟  \* @url: blog.80aj.com  \*/ function url\_encode ($string) {     $source = utf8\_decode($string); //编码转换成 iso-8859-1 编码     $ntexto = &#8220;&#8221;;     $codekey = &#8220;ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789\_-&#8221;;     for ($i = 0; $i < strlen($string); $i ++) {         // echo $string{$i} . &#8220;<br>&#8221;; //输出字符         //echo ord($string{$i}) . &#8220;<br>&#8221;; //输出字符的 ASCII  值         //exit();         $ntexto .= substr(&#8220;0000&#8243; . base\_convert(ord($string{$i}), 10, 2), &#8211; 8); //  将 ascii值 从10进制转换成 2进制 并且在头部添加 0000 截取 后8位     }     // echo $ntexto;     $ntexto .= substr(&#8220;00000&#8243;, 0, 6 &#8211; strlen($ntexto) % 6); // 取转换出来的字符串长度 取除6的余数  后面补0  保证 字符串长度为6的整数倍     $string = &#8220;&#8221;;     for ($i = 0; $i < strlen($ntexto) &#8211; 1; $i = $i + 6) {         // echo intval(substr($ntexto, $i, 6), 2) . &#8220;<br>&#8221;; // 转换去整数   将2进制 转换成10进制         $string .= $codekey{intval(substr($ntexto, $i, 6), 2)}; // 从$ntexto 截取 6位 并且 返回对应的 字符串对应的字符     }     return $string; } /\*\*  \*wp Audio Player 插件音乐地址解密函数  \*@author 荒野无灯  \*@url http://www.ihacklog.com/  \*@date 2010/04/05  \*说明：仅供学习交流之用。  */ function url\_decode ($source\_str) {     $bin\_code = &#8221;;     $str = &#8221;;     $codekey = &#8216;ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789\_-&#8217;;     $source\_len = strlen($source\_str);     for ($i = 0; $i < $source\_len; $i ++) {         $current\_strpos = strpos($codekey, substr($source\_str, $i, 1));         $sixbit\_bin = substr(&#8217;000000&#8242; . base\_convert($current\_strpos, 10, 2), &#8211; 6, 6);         $bin\_code .= $sixbit\_bin;     }     $bin\_code\_len = strlen($bin\_code);     for ($i = 0; $i < $bin\_code\_len; $i += 8) {         $eight\_bit\_bin = substr($bin\_code, $i, 8);         $ascii\_num = base\_convert($eight\_bit\_bin, 2, 10);         $str .= chr($ascii\_num);     }     return $str; } $str = url\_encode(&#8220;i love you&#8221;); echo &#8220;<br>&#8221; . $str;