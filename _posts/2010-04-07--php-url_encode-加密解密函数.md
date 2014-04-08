---
title: 100407 php url_encode 加密解密函数
layout: post
permalink: /1009.html
related_posts:
  - 'a:2:{s:4:"time";s:10:"1292192760";s:13:"related_posts";s:1929:"<ul class="related_post"><li><a href="http://blog.80aj.com/guestbook/" title="关于">关于</a></li><li><a href="http://blog.80aj.com/2010/04/15/100415-%e4%b8%80%e4%b8%aa%e5%a5%b3%e7%a8%8b%e5%ba%8f%e5%91%98%e7%9a%84%e5%be%81%e5%a9%9appt/" title="100415 一个女程序员的征婚ppt">100415 一个女程序员的征婚ppt</a></li><li><a href="http://blog.80aj.com/2010/04/08/100408-php-%e5%85%b3%e4%ba%8e-sqllite%e5%ba%94%e7%94%a8/" title="100408 php 关于 sqllite应用">100408 php 关于 sqllite应用</a></li><li><a href="http://blog.80aj.com/2010/12/04/101204-phpase-%e5%8a%a0%e5%af%86/" title="101204 phpase 加密">101204 phpase 加密</a></li><li><a href="http://blog.80aj.com/2010/10/30/101030-%e6%96%87%e4%bb%b6%e6%8a%93%e5%8f%96-snoopy%e7%b1%bb%e4%bb%8b%e7%bb%8d/" title="101030 文件抓取 snoopy类介绍">101030 文件抓取 snoopy类介绍</a></li><li><a href="http://blog.80aj.com/2010/10/29/101029-php-%e4%ba%a7%e5%93%81%e5%ae%89%e8%a3%85%e7%a8%8b%e5%ba%8f%e5%88%b6%e4%bd%9c%e4%bb%a3%e7%a0%81demo/" title="101029 php 产品安装程序制作代码demo">101029 php 产品安装程序制作代码demo</a></li><li><a href="http://blog.80aj.com/2010/10/28/101028-php%e9%a1%b5%e9%9d%a2%e6%89%a7%e8%a1%8c%e6%97%b6%e9%97%b4class/" title="101028 php页面执行时间class">101028 php页面执行时间class</a></li><li><a href="http://blog.80aj.com/2010/09/13/100913-php%e6%8b%9b%e8%81%98%e5%b9%bf%e5%91%8a%e4%b8%80%e5%88%99/" title="100913 PHP招聘广告一则">100913 PHP招聘广告一则</a></li><li><a href="http://blog.80aj.com/2010/08/22/100822-php-%e4%b9%a6%e7%b1%8d%e5%88%86%e4%ba%ab/" title="100822 php 书籍分享">100822 php 书籍分享</a></li><li><a href="http://blog.80aj.com/2010/08/21/100821-php%e4%b9%8b%e8%85%be%e8%ae%af%e5%be%ae%e5%8d%9a-api-%e4%bf%ae%e6%94%b9%e7%89%88/" title="100821 php之腾讯微博 Api 修改版">100821 php之腾讯微博 Api 修改版</a></li></ul>";}'
bot_views:
  - 89
duoshuo_thread_id:
  - 1280248249638191168
views:
  - 2
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
[<img class="aligncenter size-full wp-image-1010" title="jiamijiemi" src="http://www.80aj.com/wp-content/uploads/2010/04/jiamijiemi.jpg" alt="" width="246" height="204" />][1]  
/**  
 *wp Audio Player 插件音乐地址加密函数  
 <*@date> 2010/04/07  
 *代码阅读注释添加:  
 * @author :可乐烟  
 * @url: [blog.80aj.com][2]  
 */  
function url_encode ($string)  
{  
    $source = utf8_decode($string); //编码转换成 iso-8859-1 编码  
    $ntexto = &#8220;&#8221;;  
    $codekey = &#8220;ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789_-&#8221;;  
    for ($i = 0; $i < strlen($string); $i ++) {  
        // echo $string{$i} . &#8220;<br>&#8221;; //输出字符  
        //echo ord($string{$i}) . &#8220;<br>&#8221;; //输出字符的 ASCII  值  
        //exit();  
        $ntexto .= substr(&#8220;0000&#8243; . base_convert(ord($string{$i}), 10, 2), &#8211; 8); //  将 ascii值 从10进制转换成 2进制 并且在头部添加 0000 截取 后8位  
    }  
    // echo $ntexto;  
    $ntexto .= substr(&#8220;00000&#8243;, 0, 6 &#8211; strlen($ntexto) % 6); // 取转换出来的字符串长度 取除6的余数  后面补0  保证 字符串长度为6的整数倍  
    $string = &#8220;&#8221;;  
    for ($i = 0; $i < strlen($ntexto) &#8211; 1; $i = $i + 6) {  
        // echo intval(substr($ntexto, $i, 6), 2) . &#8220;<br>&#8221;; // 转换去整数   将2进制 转换成10进制  
        $string .= $codekey{intval(substr($ntexto, $i, 6), 2)}; // 从$ntexto 截取 6位 并且 返回对应的 字符串对应的字符  
    }  
    return $string;  
}  
/**  
 *wp Audio Player 插件音乐地址解密函数  
 <*@author> 荒野无灯  
 <*@url> <http://www.ihacklog.com/>  
 <*@date> 2010/04/05  
 *说明：仅供学习交流之用。  
 */  
function url\_decode ($source\_str)  
{  
    $bin_code = &#8221;;  
    $str = &#8221;;  
    $codekey = &#8216;ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789_-&#8217;;  
    $source\_len = strlen($source\_str);  
    for ($i = 0; $i < $source_len; $i ++) {  
        $current\_strpos = strpos($codekey, substr($source\_str, $i, 1));  
        $sixbit\_bin = substr(&#8217;000000&#8242; . base\_convert($current_strpos, 10, 2), &#8211; 6, 6);  
        $bin\_code .= $sixbit\_bin;  
    }  
    $bin\_code\_len = strlen($bin_code);  
    for ($i = 0; $i < $bin\_code\_len; $i += 8) {  
        $eight\_bit\_bin = substr($bin_code, $i, 8);  
        $ascii\_num = base\_convert($eight\_bit\_bin, 2, 10);  
        $str .= chr($ascii_num);  
    }  
    return $str;  
}  
$str = url_encode(&#8220;i love you&#8221;);  
echo &#8220;<br>&#8221; . $str;

 [1]: http://www.80aj.com/wp-content/uploads/2010/04/jiamijiemi.jpg
 [2]: http://www.80aj.com