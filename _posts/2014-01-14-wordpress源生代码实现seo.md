---
title: 140114 wordpress源生代码实现SEO
layout: post
permalink: /2696.html
categories:
  - Code
tags:
  - M2
  - seo
  - wordpress
  - 模板
  - 源生代码
---
很早之前看到macdang.com的时候，觉得这套模板很清新，比较适合coder做自己的技术博客，想把自己的博客模板也换成这个。可惜查看相关代码没有找到模板作者。昨天查看wopus的时候看到了这套模板： 原名为M2模板。作者通过最wordpress源生php代码实现了翻页，阅读计数等常见插件的功能，不过对于seo这一块并没有做，这里补充下实现wordpress 源生代码实现Seo . 以下代码替换模板代码 header.php中 部分: <?php if (is\_home ()) { $keywords = "相关关键字描述"; $description = "相关desc描述"; } elseif (is\_single ()) { if ($post->post\_excerpt) { $description = $post->post\_excerpt; } else { $str = csubstr ( strip\_tags ( $post->post\_content ), 0, 220 ); $str = trim ( $str ); $str = strip\_tags ( $str, "" ); $str = ereg\_replace ( "\t", "", $str ); $str = ereg\_replace ( "\r\n", "", $str ); $str = ereg\_replace ( "\r", "", $str ); $str = ereg\_replace ( "\n", "", $str ); $str = ereg\_replace ( " ", " ", $str ); $description = trim ( $str ); } $keywords = ""; $tags = wp\_get\_post\_tags ( $post->ID ); foreach ( $tags as $tag ) { $keywords = $keywords . $tag->name . ", "; } } ?> <title><?php global $page, $paged; wp\_title ( '|', true, 'right' ); bloginfo ( 'name' ); $site\_description = get\_bloginfo ( 'description', 'display' ); if ($site\_description && (is\_home () || is\_front\_page ())) echo " | $site\_description"; if ($paged >= 2 || $page >= 2) echo ' | ' . sprintf ( \__ ( 'Page %s' ), max ( $paged, $page ) ); ?></title> <meta name="keywords" content="<?=$keywords?>" /> <meta name="description" content="<?=$description?>" /> 本文资料: www.macdang.com mac党 主要是下载破解mac软件的，目前已经不怎么更新 www.mangguo.org m2 主题作者