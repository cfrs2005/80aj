---
title: 110525 win7x64 +wamp+pgsql
layout: post
permalink: /2108.html
categories:
  - Linux
tags:
  - pgsql
  - wamp
  - win7x64
  - 不是一个有效的win32程序
  - 依赖dll
---
尼玛的 公司换了 新电脑 win7x64的 ，装个环境折腾了我2天 不过总算有所收获 真正了解关于 扩展加载需要的dll方式 ,在这里记录以下也算是分享 启动apache 老是报错: PHP Warning:  PHP Startup: Unable to load dynamic library &#8216;d:/wamp/bin/php/php5.3.4/ext/php\_pdo\_pgsql.dll&#8217; &#8211; %1 \xb2\xbb\xca\xc7\xd3\xd0\xd0\xa7\xb5\xc4 Win32 \xd3\xa6\xd3\xc3\xb3\xcc\xd0\xf2\xa1\xa3\r\n in Unknown on line 0PHP Warning:  PHP Startup: Unable to load dynamic library &#8216;d:/wamp/bin/php/php5.3.4/ext/php\_pgsql.dll&#8217; &#8211; %1 \xb2\xbb\xca\xc7\xd3\xd0\xd0\xa7\xb5\xc4 Win32 \xd3\xa6\xd3\xc3\xb3\xcc\xd0\xf2\xa1\xa3\r\n in Unknown on line 0 &nbsp; &nbsp; 步骤1： 下载 dependency.exe 下载地址： http://www.dependencywalker.com/ &nbsp; 步骤2: 打开php\_pgsql.dll 如图所示: 即可看到 php_pgsql.dll 需要依赖的dll 并且还能知道依赖的.dll需要其他的支持 &nbsp; win7 x64 pgsql 所需的dll 安装pgsql 9.0 x64  将 bin目录下 如下文件  复制到    windows/system32 下重新启动即可 libeay32.dll libintl.dll libpq.dll ssleay32.dll