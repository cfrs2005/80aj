---
title: 140127 wordpress可视化优化
layout: post
permalink: /2729.html
views:
  - 27
ta-thumbnail:
  - NoMediaFound
categories:
  - Code
tags:
  - wordpress
  - wp_deregister_script
  - 优化
---
优化是基于lnmp架构的系统，用户访问前端访问加速的优化。并不适合所有用户。

### wordpress主题优化

<pre>取消头部内容加载</pre>

<pre class="brush: php; title: ; notranslate" title="">//头部取消wordpress自带jquery加载
//修改当前模板 header.php 在 wp_head();增加
wp_deregister_script("jquery");

//主题function.php里增加下方代码,去掉一些没有必要的内容加载
remove_action('wp_head', 'rsd_link');
remove_action('wp_head', 'wlwmanifest_link');
remove_action('wp_head', 'wp_generator');


</pre>

### wordpress图片优化

<pre><b>LNMP开启对于图片的gzip压缩支持</b>
修改文件 /usr/nginx/conf/nginx.conf增加红色部分
gzip_types text/plain application/x-javascript text/css application/xml <font color="red">image/jpeg image/gif image/png</font>;

<b>资源图片优化</b>

http://zhanzhang.baidu.com/optimization/index?site=http://www.m2277.com/

</pre>

### wordpress样式优化

利用PHP &#8211; Minify优化css,js进行请求压缩。  
**下载minify包 http://pan.baidu.com/s/1bn6BLIf**

<pre class="brush: php; title: ; notranslate" title="">//将解压缩后的包min放入主题目录下，注意：当前wordpress需要开启urlwrite
//具体引用CSS放头部 header.php
&lt;link rel="stylesheet" href="&lt;?php bloginfo('template_url');?&gt;/min/?b=&lt;?php echo str_replace(get_bloginfo('home') . '/', '', get_bloginfo('template_directory')); ?&gt;/assets&f=reset.css,mangguo.css"&gt;


//具体引用JS放底部 footer.php
&lt;script charset="utf-8" src="&lt;?php bloginfo('template_url');?&gt;/min/?b=&lt;?php echo str_replace(get_bloginfo('home') . '/', '', get_bloginfo('template_directory')); ?&gt;/assets&f=jquery.min.js,jquery.cookie.js,mangguo.js"&gt;&lt;/script&gt;

</pre>

### wordpress插件缓存优化

<pre>后台安装 wp-super-cache，<b>开启预加载</b>。会有点击数不增加BUG，不过这个不是很关注。我们都会用百度,cnnz之类的统计代码。
关于: <b>memcached,redis,Varnish等等是能给wordpress减少大量的db请求,但本质上没有解决用户秒开的问题，所以我没有使用。</b>
</pre>

### 非本主题相关

<pre class="brush: php; title: ; notranslate" title="">//修改wp-config.php,取消后台编辑文章的修订功能
define('WP_POST_REVISIONS', false);
</pre>