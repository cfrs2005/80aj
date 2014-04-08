---
title: '130423 jquery  textarea append bug'
author: 张 清月
layout: post
permalink: /2592.html
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
views:
  - 801
post_views_count:
  - 0
duoshuo_thread_id:
  - 1280248249638191380
categories:
  - Code
tags:
  - append
  - bug
  - jquery
  - textarea
---
一连串的英文 只是因为 遇到这样的问题 真心无语

在 jquery 插件 使用的时候 

textarea append 时而有效 时而无效 ，强迫者使用者 刷新页面 再次适用 ，这不是我的本意。

<pre class="brush: xml; title: ; notranslate" title="">//问题代码
&lt;textarea id="description"&gt;&lt;/textarea&gt;
&lt;script language="javascript"&gt;
    $("#description").append(txt);
&lt;/script&gt;


//实际解决
&lt;script language="javascript"&gt;
    $("#description").val($('#description').val() + "text");
&lt;/script&gt;
</pre>