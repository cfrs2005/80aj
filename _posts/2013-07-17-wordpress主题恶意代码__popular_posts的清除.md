---
title: 130717 wordpress 主题恶意代码 __popular_posts 的清除
layout: post
permalink: /2617.html
categories:
  - Code
tags:
  - wordpress
  - __popular_posts
  - 主题
  - 感染
  - 清理
---
安装完主题以后 出现了 500错误，而又无从下手 或许本文可以帮助到你 主题使用久了 总没新鲜感，随上了点社区论坛之类的，找了几个主题下载。装了上去，之前也没什么反映，突然一下子就出现了500错误。 悲催的 nginx -error-log 和 apache-error-log 毫无反映。 尝试调整代码 error\_reporting() 解决 发现也有太多 地方直接强制把注释改为了 0 伤感。 清理思路： 1：查看 当前使用的主题 路径 登陆mysql 查看 options 表中 的 template ，因为我一直也没有太关注 关于主题字段的名字，随便猜测了下 结果中了 SELECT * FROM wp\_options WHERE \`option\_name\` LIKE '%temp%' LIMIT 0 , 30 wordpress 中使用 wp-options 中 使用 字段名 为 template 的 来存储当前博客使用的 主题路径。 2: 将错误主题 替换为 之前试用过的 或者是正常的主题。 简单的mv mv 依然还是错误。。 3：无解的时候 看了下 为什么 各种日志为什么不打印 php错误日志。 php.ini 中 display\_errors = off 被设置关闭了 4: 直接在 wordpress 的index.php中强制开启 disaply\_errors ini\_set('display\_errors', 'on'); 5:看到了 万年前邪恶错误代码 Fatal error: Cannot redeclare \_\_popular\_posts() (3 posts) 这个自我复制 修改 themes 目录下所有 functions.php 代码 实在是太恶心了 6:确认目录下所有 主题都已经被感染，瞬间有种蛋疼到家的感觉 将所有 主题 移除。 留一份 当前使用的 清理掉 functions.php 中 对应的 自我复制代码。 到此结束，最后找了篇 关于 代码解释的 希望你喜欢。 呃 其实也没什么，只是感觉很悲催的样子，前段时间 还在某群里 咆哮 君，作为一个技术人员你都能QQ中毒不耻辱么 哎。 恶意病毒代码解读： http://www.chukuangren.com/wordpress-zhongdu.html 恶意病毒代码完整版： http://wpcme.com/pics/01204/wordpress-malicious-code.html