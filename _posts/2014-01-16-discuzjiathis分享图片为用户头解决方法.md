---
title: 140116 discuz jiathis分享图片为用户头解决方法
layout: post
permalink: /2704.html
categories:
  - Code
tags:
  - discuz
  - jiathis
  - 分享
  - 用户头像
---
jiathis的图片分享的时候，并没有主动设置需要分享的图片这里给个简单的discuz代码解决分享图片问题。 修改模板文件： template/default/forum/viewthread\_node.htm <!--{if !IS\_ROBOT}--> <!--{if !$postcount && !$\_G\['forum\_thread'\]\['archiveid'\] && $post\['first'] }--> //新增开始 <!--{if !$postcount && !$\_G['forum\_thread'\]\['archiveid'\] && $post['first'] }--> <!--{eval $i =0}--> <!--{loop $post[attachments] $att}--> <!--{if $i < 5}--> <!--{if $att['isimage']==1}--> <!--{eval $threadattachmenturl[] = $att['url'].$att['attachment']; }--> <!--{/if}--> <!--{/if}--> <!--{eval $i++}--> <!--{/loop}--> //新增结束 jiathis代码下方增加： <script type="text/javascript" > <!--{if $threadattachmenturl != null}--> var jiathis_config = { 'pic':'{echo implode('||',$threadattachmenturl)}' }; <!--{/if}--> </script>