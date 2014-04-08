---
title: Discuz 常见问题
layout: page
---
### 基于DiscuzX3修改,做备忘录  
### <pre>对不起，您安装的不是正版应用，安装程序无法继续执行</pre>

<pre class="brush: php; title: ; notranslate" title="">//编辑 source/function/function_cloudaddons.php 搜索 cloudaddons_genuine_message.注释代码
//cpmsg('cloudaddons_genuine_message', '', 'error',array('addonid' =&gt;$addonid));}}
</pre>

<pre>密码错误次数过多，请15 分钟后重新登录！</pre>

<pre class="brush: php; title: ; notranslate" title="">//编辑 source/function/function_member.php
$return = (!$login || (TIMESTAMP - $login['lastupdate'] &gt; 900)) ? 5 : max(0, 5 - $login['count']);
//900替换为你想要的时间
</pre>

或者

<pre class="brush: php; title: ; notranslate" title="">//sql直接执行,清除cookie
delete from pre_common_failedlogin;
</pre>