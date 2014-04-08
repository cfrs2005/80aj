---
title: 130419 mac os vim style 开启
layout: post
permalink: /2589.html
categories:
  - Linux
tags:
  - macos
  - style
  - vim
  - 开启
---
macos 的 vim 实在是太淳朴了 淳朴的 让人 使用不下去。  
简单10秒让你的vim 精彩起来。 如下是如何开启 macos vim style的过程

<pre class="brush: bash; title: ; notranslate" title="">//进去命令终端 我一般喜欢 spotlight 搜索出来  
// 按键  contorl+空格 搜搜 ter 就出来 命令终端了
//切换到root用户


sudo su -

//编辑配置文件

vim /usr/share/vim/vimrc 

//将下面代码贴入文档最后面 保存即可

set ai                  " auto indenting
set history=100         " keep 100 lines of history
set ruler               " show the cursor position
syntax on               " syntax highlighting
set hlsearch            " highlight the last searched term
filetype plugin on      " use the file type plugins

" When editing a file, always jump to the last cursor position
autocmd BufReadPost *
\ if ! exists("g:leave_my_cursor_position_alone") |
\ if line("'\"") &gt; 0 && line ("'\"") &lt;= line("$") |
\ exe "normal g'\"" |
\ endif |
\ endif
</pre>

编辑文件即可看到 如下截图效果显示:

[<img src="http://pic.80aj.com/2013/04/cmd-300x244.jpg" alt="cmd" width="300" height="244" class="aligncenter size-medium wp-image-2591" />][1]

 [1]: http://pic.80aj.com/2013/04/cmd.jpg