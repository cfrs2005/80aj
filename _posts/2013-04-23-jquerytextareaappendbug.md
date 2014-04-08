---
title: '130423 jquery  textarea append bug'
layout: post
permalink: /2592.html
categories:
  - Code
tags:
  - append
  - bug
  - jquery
  - textarea
---
一连串的英文 只是因为 遇到这样的问题 真心无语 在 jquery 插件 使用的时候 textarea append 时而有效 时而无效 ，强迫者使用者 刷新页面 再次适用 ，这不是我的本意。 //问题代码 <textarea id="description"></textarea> <script language="javascript"> $("#description").append(txt); </script> //实际解决 <script language="javascript"> $("#description").val($('#description').val() + "text"); </script>