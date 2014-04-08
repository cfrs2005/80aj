---
title: 140218 wp-postviews,wp-supercache冲突解决
layout: post
permalink: /2746.html
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
wp-postviews,wp-supercache冲突 很多时候博客为了加速访问会安装wp-supercache来解决访问速度问题，但糟糕的是大部分人在使用的时候发现wp-postviews使用失效了，然后网上搜索了一大堆无效的代码文章，并且并不能正确的解决该问题。自己查看了调用代码，找到了具体原因： 本质上wp-postviews已经解决了wp-supercache的冲突，但是很多主题作者为了解决多次调用jquery,或者jquery加速问题会自己另外加载jquery，并且主题里增加： wp\_deregister\_script("jquery"); 从而做到不加载wordpress自带jquery: <script type='text/javascript' src='http://www.lewafan.com/wp-includes/js/jquery/jquery.js?ver=1.10.2'></script> <script type='text/javascript' src='http://www.lewafan.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=1.2.1'></script> 解决此类冲突： //修改:plugins/wp-postviews/wp-postviews.php 847行 wp\_enqueue\_script('wp-postviews-cache', plugins\_url('postviews-cache.js', \\_\_FILE\_\_), array('jquery'), '1.64',true); //修改为: wp\_enqueue\_script('wp-postviews-cache', plugins\_url('postviews-cache.js', \\_\_FILE\_\_), false, '1.64',true); wp\_enqueue\_script wordpress使用介绍 wp\_enqueue\_script( $handle, $src, $deps, $ver, $in\_footer ) 参数 $handle （字符串）（必需）脚本名称。小写字符串。 默认值：None $src （字符串）（可选）WordPress根目录下的脚本路径 示例："/wp-includes/js/scriptaculous/scriptaculous.js"。该参数只在WordPress不了解脚本情况时使用。 默认值：None $deps （数组）（可选）脚本所依靠的句柄组成的数组；加载该脚本前需要加载的其它脚本。若没有依赖关系，返回false。该参数只在WordPress不了解脚本情况时使用。 默认值：array() $ver （字符串）（可选）指明脚本版本号的字符串（若存在版本号）。默认为false。该参数可确保即使在启用缓存的状态下，发送给客户端的仍然是正确版本，因此如果版本号可用且对脚本有意义，包含该版本号。 默认值：false $in\_footer （布尔型）（可选）通常情况下脚本会被放置在区块中。如果该函数为true，脚本则会出现在区块的最下方。要求主题在适当的位置中包含有wp\_footer()钩子。（WordPress新功能） 默认值：false wp\_enqueue\_script使用demo: add\_action('wp\_enqueue\_scripts', 'wp\_postview\_cache\_count\_enqueue'); function wp\_postview\_cache\_count\_enqueue() { wp\_enqueue\_script('wp-postviews-cache', plugins\_url('postviews-cache.js', \\_\_FILE\_\_), false, '1.64',true); wp\_localize\_script('wp-postviews-cache', 'viewsCacheL10n', array('admin\_ajax\_url' => admin\_url('admin-ajax.php', (is\_ssl() ? 'https' : 'http')), 'post\_id' => intval($post->ID))); } 相关资料: http://codex.wordpress.org/Function\_Reference/wp\_enqueue\_script http://www.wordpress.la/codex-%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0-wp\_enqueue\_script().html