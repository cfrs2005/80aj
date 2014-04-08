---
title: 120914 href title 无效 这个真心不能算是个BUG
layout: post
permalink: /2325.html
categories:
  - Code
tags:
  - bug
  - href
  - html
  - ie8
  - 不显示
---
[<img src="http://www.80aj.com/wp-content/uploads/2012/09/htmlbug.jpg" alt="" title="htmlbug" width="321" height="107" class="aligncenter size-full wp-image-2326" />][1]

ie8 会发现给 超链接加了 href 后 title 失效 实际上是 代码格式问题 而不是 a 元素里不能放东西：）

<pre lang="html">//正确用法
<a title="50元电影网" target="_blank" href="http://www.50y.cc">
<b>50元电影网</b>
</a>
<br />

//错误用法
<a title="50元电影网" target="_blank" href="http://www.50y.cc"><b>50元电影网</b></a>
</pre>

 [1]: http://www.80aj.com/wp-content/uploads/2012/09/htmlbug.jpg