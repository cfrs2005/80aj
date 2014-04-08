---
title: '120914  警惕  slides.min.jquery.js'
layout: post
permalink: /2327.html
bot_views:
  - 59
views:
  - 544
duoshuo_thread_id:
  - 1280248249638191316
categories:
  - Code
tags:
  - bug
  - js插件
  - slides插件
  - 图片2次请求
  - 图片有时间戳
---
[<img src="http://www.80aj.com/wp-content/uploads/2012/09/slider2s.jpg" alt="" title="slider2s" width="406" height="293" class="aligncenter size-full wp-image-2328" />][1]

警惕 slides.min.jquery.js 

* Slides, A Slideshow Plugin for jQuery  
* Intructions: http://slidesjs.com  
* By: Nathan Searles, http://nathansearles.com  
* Version: 1.1.9  
* Updated: September 5th, 2011 

在优化首页的时候遇到个问题 

源代码中 查看图片是 正常的 

<pre lang="html"><img src="yuanjian.jpg" />
</pre>

可是在firefox 下面访问得时候 就成了 带有时间戳

<pre lang="html"><img src="yuanjian.jpg?1237981298" />
</pre>

这本来没什么 可是作为优化网站工作的一部分 多一次访问 就是一次损耗 对于一个流量比较大的网站来说 这就是一笔开销 

<pre lang="js">//js 关键代码：
var z = d.find("img:eq(" + h + ")").attr("src");  //关键代码
a("img", c).parent().attr("class") != "slides_control" ? t = d.children(":eq(0)")[0].
tagName.toLowerCase() : t = d.find("img:eq(" + h + ")"),
d.find("img:eq(" + h + ")").attr("src", z).load(function() {   //关键代码
    d.find(t + ":eq(" + h + ")").fadeIn(
    b.fadeSpeed, b.fadeEasing,
    function() {
        a(this).css({
            zIndex: 5
        }),
        a("." + b.container, c).css({
            background: ""
        }),
        o = !0,
        b.slidesLoaded()
    })
})
} else d.children(":eq(" + h + ")").fadeIn(b.fadeSpeed, b.fadeEasing,
function() {
    o = !0,
    b.slidesLoaded()
});
</pre>

 [1]: http://www.80aj.com/wp-content/uploads/2012/09/slider2s.jpg