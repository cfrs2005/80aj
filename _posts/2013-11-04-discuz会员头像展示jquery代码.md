---
title: '131104 discuz 会员头像展示 &#8211; jquery 代码'
layout: post
permalink: /2657.html
categories:
  - Code
tags:
  - discuz会员
  - jquery
  - jquery HTMLDivElement
  - 展示
---
jquery的使用级别 我一直停留在简单应用，是非常大的弱项，很可悲。  
**特别是 div 层的图片滚动的计算 **。 写这个只是为了赞美 某强大 的JS工程师 <a href="http://blog.taochengzhou.com/" target="_blank">桃子</a> .

**discuz会员头像展示主要功能: **  
将一组A标签 以6个为单位分割 并且组建新的div 进行互换展示 支持鼠标的停留

**discuz会员头像展示效果图片:**

[<img src="http://pic.80aj.com/2013/11/jsxiaoguo-110x110.jpg" alt="jsxiaoguo" width="110" height="110" class="aligncenter size-medium wp-image-2659" />][1] 

discuz会员头像展示代码:

<pre class="brush: jscript; title: ; notranslate" title="">lewaStar=function(){
		var targetArea=$("#fly_stars");
		alert(targetArea);
		var elems = $('.lewabbs-star'), parts = [],i=0;
		do{
			parts[i] = elems.splice(0,6);
			$('&lt;div class="star-block"&gt;&lt;/div&gt;').append(parts[i]).appendTo(targetArea);
			i++;
		}while(elems.length&gt;0);
		var objs = $('.star-block');
		var t,	 time = 200, delay = 4000, curr = 0,call_x = function(){
			$(objs[curr]).fadeOut(time, call_y);
		}, call_y = function(){
			curr ++;
			if(curr &gt;= objs.length) curr=0;
			$(objs[curr]).fadeIn();
			t = setTimeout(call_x, delay);
		};
		objs.mouseover(function(){
			if(t) clearTimeout(t);
		});
		objs.mouseout(function(){
			t = setTimeout(call_x, delay);
		});
		call_x();
	}
</pre>

**discuz会员头像展示主要过程:**

1:timer 定时器的 触发轮换  
2:鼠标的 onmouse 和mouseout 处理  
3:jquery [object Object] 和 jquery [object HTMLDivElement] 的处理

**附加一篇关于 jquery [object Object] 和 jquery [object HTMLDivElement] 的处理 的文章 :**

来源:

http://www.cnblogs.com/daisuki/archive/2013/04/04/2999745.html

在使用jQuery时，发现有两种对象，一个是[object Object]，另一个是就像[object HTMLDivElement]

**前者是jQuery对象，通过jQuery的选择器$(&#8216;selector&#8217;)获得；  
后者是DOM元素，为 javascript中的getElementById, getElementsByTagName等方法的返回类型。  
**  
只有jQuery对象才能使用jQuery的一系列方法，DOM元素是不能用的。 其实，jQuery对象就类似一个数组，它包含了一个或多个与jQuery选择器匹配的DOM元素。

<pre class="brush: jscript; title: ; notranslate" title="">//一个js获取的标签为li的元素数组
var normalArray = document.getElementsByTagName('li');  

//相当于上面的，但是是一个jQuery对象
var jQueryArray = $('li');

//如果是由元素Id获得DOM元素的话，则jQuery对象就像一个长度为1的数组。
//比如，以下三个alert的结果是相同的
alert(document.getElementById('myID'));
alert($('#myID')[0]);
alert($('#myID').get(0));

//*** jQuery对象与DOM元素之间的转换 ***

//返回与 jQuery 选择器匹配的DOM元素的数量
jQueryArray.length;
jQueryArray.size();

//从jQuery对象获得普通的DOM集合，[&lt;li id="foo"&gt;, &lt;li id="bar"&gt;]
jQueryArray.get();
jQueryArray.toArray();

//根据index获取数组中的某个元素
jQueryArray.get(index);
jQueryArray[index];

//当index是-1时，由于负数index是从数组最后开始算，所以返回数组的最后一个元素
jQueryArray.get(-1);

//当从一个jQuery对象获得一个DOM元素后，把该元素再转变成一个jQuery对象，以便调用jQuery的方法
$(jQueryArray[0]);
</pre>

 [1]: http://pic.80aj.com/2013/11/jsxiaoguo.jpg