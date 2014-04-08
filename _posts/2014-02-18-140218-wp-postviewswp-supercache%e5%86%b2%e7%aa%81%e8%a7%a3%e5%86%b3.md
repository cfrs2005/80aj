---
title: 140218 wp-postviews,wp-supercache冲突解决
author: 张 清月
layout: post
permalink: /2746.html
views:
  - 37
categories:
  - Code
tags:
  - jquery
  - wp-postviews
  - wp-supercache
  - 冲突
  - 失效
  - 解决
---
### wp-postviews,wp-supercache冲突

很多时候博客为了加速访问会安装wp-supercache来解决访问速度问题，但糟糕的是大部分人在使用的时候发现wp-postviews使用失效了，然后网上搜索了一大堆无效的代码文章，并且并不能正确的解决该问题。自己查看了调用代码，找到了具体原因：

本质上wp-postviews已经解决了wp-supercache的冲突，但是很多主题作者为了**<font color="red">解决多次调用jquery,或者jquery加速</font>**问题会自己另外加载jquery，并且主题里增加：

<pre class="brush: php; title: ; notranslate" title="">wp_deregister_script("jquery");
</pre>

从而做到不加载wordpress自带jquery:

<pre class="brush: php; title: ; notranslate" title="">&lt;script type='text/javascript' src='http://www.lewafan.com/wp-includes/js/jquery/jquery.js?ver=1.10.2'&gt;&lt;/script&gt;
&lt;script type='text/javascript' src='http://www.lewafan.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=1.2.1'&gt;&lt;/script&gt;
</pre>

### 解决此类冲突：

<pre class="brush: php; title: ; notranslate" title="">//修改:plugins/wp-postviews/wp-postviews.php 847行
wp_enqueue_script('wp-postviews-cache', plugins_url('postviews-cache.js', __FILE__), array('jquery'), '1.64',true);
//修改为:
wp_enqueue_script('wp-postviews-cache', plugins_url('postviews-cache.js', __FILE__), false, '1.64',true);
</pre>

### wp\_enqueue\_script wordpress使用介绍

<pre>wp_enqueue_script( $handle, $src, $deps, $ver, $in_footer )


参数

$handle

（字符串）（必需）脚本名称。小写字符串。

默认值：None

$src

（字符串）（可选）WordPress根目录下的脚本路径

示例："/wp-includes/js/scriptaculous/scriptaculous.js"。该参数只在WordPress不了解脚本情况时使用。

默认值：None

$deps

（数组）（可选）脚本所依靠的句柄组成的数组；加载该脚本前需要加载的其它脚本。若没有依赖关系，返回false。该参数只在WordPress不了解脚本情况时使用。

默认值：array()

$ver

（字符串）（可选）指明脚本版本号的字符串（若存在版本号）。默认为false。该参数可确保即使在启用缓存的状态下，发送给客户端的仍然是正确版本，因此如果版本号可用且对脚本有意义，包含该版本号。

默认值：false

$in_footer

（布尔型）（可选）通常情况下脚本会被放置在<head>
  区块中。如果该函数为true，脚本则会出现在区块的最下方。要求主题在适当的位置中包含有wp_footer()钩子。（WordPress新功能）
  
  默认值：false
  </pre>
  <h3>
    wp_enqueue_script使用demo:
  </h3>
  
  
  <pre class="brush: php; title: ; notranslate" title="">
add_action('wp_enqueue_scripts', 'wp_postview_cache_count_enqueue');
function wp_postview_cache_count_enqueue() {
    wp_enqueue_script('wp-postviews-cache', plugins_url('postviews-cache.js', __FILE__), false, '1.64',true);
    wp_localize_script('wp-postviews-cache', 'viewsCacheL10n', array('admin_ajax_url' =&gt; admin_url('admin-ajax.php', (is_ssl() ? 'https' : 'http')), 'post_id' =&gt; intval($post-&gt;ID)));  
}
</pre>
  
  
  <h3>
    相关资料:
  </h3>
  
  
  <p>
    http://codex.wordpress.org/Function_Reference/wp_enqueue_script
  </p>
  
  
  <p>
    http://www.wordpress.la/codex-%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0-wp_enqueue_script().html
  </p>