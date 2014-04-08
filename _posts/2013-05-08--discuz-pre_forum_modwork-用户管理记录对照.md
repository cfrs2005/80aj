---
title: 130508 discuz pre_forum_modwork 用户管理记录对照
layout: post
permalink: /2597.html
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
views:
  - 22389
post_views_count:
  - 0
duoshuo_thread_id:
  - 1280248249638191383
ta-thumbnail:
  - NoMediaFound
categories:
  - Code
tags:
  - cls
  - discuz
  - edt
  - pre_forum_modwork
---
discuz 关于 统计管理员操作记录表 有哪些行为被记录 并且成为管理记录的 

中英文对照 

<pre class="brush: php; title: ; notranslate" title="">'EDT' =&gt; '编辑',

	'DEL' =&gt; '删除',
	'DLP' =&gt; '删除回复',
	'DCM' =&gt; '删除点评',
	'PRN' =&gt; '批量删帖',
	'UDL' =&gt; '反删除',

	'DIG' =&gt; '加入精华',
	'UDG' =&gt; '解除精华',
	'EDI' =&gt; '限时精华',
	'UED' =&gt; '解除限时精华',

	'CLS' =&gt; '关闭',
	'OPN' =&gt; '打开',
	'ECL' =&gt; '限时关闭',
	'UEC' =&gt; '解除限时关闭',
	'EOP' =&gt; '限时打开',
	'UEO' =&gt; '解除限时打开',

	'STK' =&gt; '置顶',
	'UST' =&gt; '解除置顶',
	'EST' =&gt; '限时置顶',
	'UES' =&gt; '解除限时置顶',

	'SPL' =&gt; '分割',
	'MRG' =&gt; '合并',

	'HLT' =&gt; '设置高亮',
	'UHL' =&gt; '解除高亮',
	'EHL' =&gt; '限时高亮',
	'UEH' =&gt; '解除限时高亮',

	'BMP' =&gt; '提升',
	'DWN' =&gt; '下沉',

	'MOV' =&gt; '移动',
	'CPY' =&gt; '复制',
	'TYP' =&gt; '分类',

	'RFD' =&gt; '强制退款',

	'MOD' =&gt; '审核通过',

	'ABL' =&gt; '加入文集',
	'RBL' =&gt; '移除文集',

	'PTS' =&gt; '推送主题',
	'RFS' =&gt; '解除推送',
	'RMR' =&gt; '取消悬赏',
	'BNP' =&gt; '屏蔽帖子',
	'UBN' =&gt; '解除屏蔽',

	'REC' =&gt; '推荐',
	'URE' =&gt; '解除推荐',

	'WRN' =&gt; '警告',
	'UWN' =&gt; '解除警告',

	'SPA' =&gt; '鉴定为',
	'SPD' =&gt; '撤销鉴定',

	'REG' =&gt; '群组推荐',
</pre>

查询单个用户的管理记录

<pre class="brush: php; title: ; notranslate" title="">select uid, SUM(count) from pre_forum_modwork  where uid =1 and dateline &gt; '2013-04-30' ;
</pre>