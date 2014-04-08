---
title: 140312 discuz帖子内容还原HTML
layout: post
permalink: /2766.html
views:
  - 16
categories:
  - Code
tags:
  - discuz
  - parseattach
---
最近挖了个坑把自己埋得差不多了，唉，说点什么好呢？太lower么

新功能需要还原贴内信息，同步到其他系统。网上看了下并没有相关内容，并且有不少遇到了**parseattach**还原问题。这里发下我解决的代码：

### 关于贴内附件还原discuz原始方法：

<pre class="brush: php; title: ; notranslate" title="">$tid=181281;
$pid=4645197;
$aid=190137;
$pids = array (
$pid 
);
$attachs = array (
$pid =&gt; array (
$aid 
) 
);
$list = array (
$pid =&gt; array (
'message' =&gt; '嘀嗒嘀嗒嘀嗒嘀嗒嘀嗒嘀嗒的 的的的 的 &lt;br /&gt;[attach]190137[/attach]&lt;br /&gt;',
'pid' =&gt; $pid,
'attachments' =&gt; array () 
) 
);
require_once libfile ( 'function/attachment' );
$_G ['tid'] = $tid;
parseattach ( $pids, $attachs, $list );
var_dump($list);
</pre>

### 改良过得帖子内容还原

<pre class="brush: php; title: ; notranslate" title="">/**
*@param: 处理discuz帖子还原相关代码demo
*@desc : 2个函数去作为获取附件并且返回附件url参数最后替换attach
*/
$thread_info = DB::fetch_first ( "select a.`tid`, a.`authorid`, a.`author`,a.`dateline`, a.`subject`, b.`message` from " . DB::table ( 'forum_thread' ) . " as a, " . DB::table ( 'forum_post' ) . " as b where a.tid=$tid and a.tid=b.tid and b.first=1 order by pid desc limit 1" );

require_once libfile ( 'function/discuzcode' );

$thread_info ['dateline'] = date ( "Y-m-d H:i:s", $thread_info ['dateline'] );
$thread_info ['message'] = discuzcode ( $thread_info ['message'] );

if (preg_match_all ( "/\[attach\](\d+)\[\/attach\]/i", $thread_info ['message'], $matchaids )) {
$attach_ids = $matchaids [1];
}
$attach_list = array ();
foreach ( $attach_ids as $aid ) {
$find = "/\[attach\]$aid\[\/attach\]/i";
$thread_info ['message'] = preg_replace ( $find, get_lw_attach_path ( $aid ), $thread_info ['message'], 1 );
$thread_info ['message'] = preg_replace ( $find, '', $thread_info ['message'] );

}



function get_lw_attach_path($aid) {
global $_G;
$return = $filename = '';
if ($attach = C::t ( 'forum_attachment_n' )-&gt;fetch ( 'aid:' . $aid, $aid, array (1,- 1) )) {
return get_lw_attach_path_str ( $attach );
}
return $filename;
}
function get_lw_attach_path_str($attach) {
global $_G;

if (! $attach ['isimage']) {
return '&lt;a href="' . $_G ['siteurl'] . 'forum.php?mod=attachment&aid=' . aidencode ( $attach ['aid'] ) . '"&gt;' . $attach ['filename'] . '&lt;/a&gt;';
}
if ($attach ['remote']) {
$imgurl = $_G ['setting'] ['ftp'] ['attachurl'] . 'forum/' . $attach ['attachment'];

return '&lt;p&gt;&lt;img onclick="viewimage(this);" src="' . $imgurl . '" /&gt;&lt;/p&gt;';
} else {
if (preg_match ( '/^(?!http:)/', $attach ['url'] )) {
$attach ['url'] = $_G ['siteurl'] . 'data/attachment/forum/' . $attach ['url'];
}
$imgurl = $attach ['url'] . $attach ['attachment'] . ($_G ['gp_width'] ? '&width=' . $_G ['gp_width'] : '') . ($_G ['gp_height'] ? '&height=' . $_G ['gp_height'] : '');

return '&lt;p&gt;&lt;a href="' . $imgurl . '" target="_blank"&gt;&lt;img height="320" width="320" src="' . $imgurl . '" /&gt;&lt;/a&gt;&lt;/p&gt;';
}

}
</pre>