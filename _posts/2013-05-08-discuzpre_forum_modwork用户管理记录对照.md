---
title: 130508 discuz pre_forum_modwork 用户管理记录对照
layout: post
permalink: /2597.html
categories:
  - Code
tags:
  - cls
  - discuz
  - edt
  - pre_forum_modwork
---
discuz 关于 统计管理员操作记录表 有哪些行为被记录 并且成为管理记录的 中英文对照 'EDT' => '编辑', 'DEL' => '删除', 'DLP' => '删除回复', 'DCM' => '删除点评', 'PRN' => '批量删帖', 'UDL' => '反删除', 'DIG' => '加入精华', 'UDG' => '解除精华', 'EDI' => '限时精华', 'UED' => '解除限时精华', 'CLS' => '关闭', 'OPN' => '打开', 'ECL' => '限时关闭', 'UEC' => '解除限时关闭', 'EOP' => '限时打开', 'UEO' => '解除限时打开', 'STK' => '置顶', 'UST' => '解除置顶', 'EST' => '限时置顶', 'UES' => '解除限时置顶', 'SPL' => '分割', 'MRG' => '合并', 'HLT' => '设置高亮', 'UHL' => '解除高亮', 'EHL' => '限时高亮', 'UEH' => '解除限时高亮', 'BMP' => '提升', 'DWN' => '下沉', 'MOV' => '移动', 'CPY' => '复制', 'TYP' => '分类', 'RFD' => '强制退款', 'MOD' => '审核通过', 'ABL' => '加入文集', 'RBL' => '移除文集', 'PTS' => '推送主题', 'RFS' => '解除推送', 'RMR' => '取消悬赏', 'BNP' => '屏蔽帖子', 'UBN' => '解除屏蔽', 'REC' => '推荐', 'URE' => '解除推荐', 'WRN' => '警告', 'UWN' => '解除警告', 'SPA' => '鉴定为', 'SPD' => '撤销鉴定', 'REG' => '群组推荐', 查询单个用户的管理记录 select uid, SUM(count) from pre\_forum\_modwork where uid =1 and dateline > '2013-04-30' ;