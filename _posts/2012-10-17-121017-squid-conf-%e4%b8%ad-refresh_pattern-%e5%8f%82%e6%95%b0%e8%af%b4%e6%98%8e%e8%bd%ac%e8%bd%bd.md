---
title: '121017 squid.conf 中 refresh_pattern 参数说明[转载]'
author: 张 清月
layout: post
permalink: /2339.html
bot_views:
  - 6
duoshuo_thread_id:
  - 1280248249638191322
views:
  - 0
categories:
  - Linux
tags:
  - override-expire
  - refresh_pattern
  - reload-into-ims
  - squid.conf
  - 参数
---
<span style="color: #ff0000;"><strong>refresh_pattern</strong></span> : 只对原始内容【即原始服务器】头部没有设置Expires过期时间的页面起作用，比如论坛页面；而对类似apache mod_expires 设置过的页面不起作用。

说明之前，先将个概念LM，LM就是页面Header里时间(Date)和Last-Modified时间的差。Date一般是Squid从后面取页面的时间，Last-Modified 一般是页面生成时间。

用于确定一个页面进入cache后,它在cache中停留的时间.refresh_pattern 规则仅仅应用到没有明确过时期限的响应.原始服务器能使 用 Expires 头部,或者 Cache-Control:max-age 指令来指定过时期限 ,只要没有在设置 override-expire.

**refresh_pattern语法：**

<pre>refresh_pattern [-i] regexp min percent max [options]
</pre>

min 参数是分钟数量.它是过时响应的最低时间限制.如果某个响应驻留在 cache 里的时间没有超过这个最低限制,那么它不会过期.类似的,max 参数是存活响应的最高时间限制.如果某个响应驻留在 cache 里的时间高于这个最高限制,那么它必须被刷新.

在最低和最高时间限制之间的响应,会面对 squid 的最后修改系数 LM-factor 算法 LM-factor=(response age)/(resource age).对这样的响应,squid 计算响应的年龄和最后修改系数,然后将它作为百分比值进行比较.响应年龄简单的就是从原始服务器产生,或最后一次验证响应后,经历的时间数量.源年龄在 Last-Modified 和 Date头 部之间是不同的.LM-factor 是响应年龄与源年龄的比率.这个基本不用详细了解,这是不是一个精确控制过期的参数,如果要精确控制过期,就不要使用这个.

**refresh_pattern参数**

我讲讲常用的几个参数的意思

<pre>override-expire
</pre>

该选项导致 squid 在检查 Expires 之前,先检查 min 值.这样,一个非零的 min 时间让 squid 返回一个未确认的 cache 命中,即使该响应准备过期.

<pre>override-lastmod
</pre>

改选项导致 squid 在检查 LM-factor 百分比之前先检查min ,它生效在expire 之后

<pre>reload-into-ims
</pre>

该选项让 squid 在确认请求里,以 no-cache 指令传送一个请求.换句话说,squid 在转发请求之前,对该请求增加一个 If-Modified- Since 头部.注意这点仅仅在目标有 Last-Modified 时间戳时才能工作.外面进来的请求保留 no-cache 指令,以便它到达原始服务器.

一般情况可以使用 reload-into-ims.它其实是强行控制对象的超时时间,这违反了http协议的精神,但是在带宽较窄的场合,可以提高明显系统相应时间.

举例：

<pre>refresh_pattern -i \.css$ 1440 50% 129600 reload-into-ims

refresh_pattern -i \.xml$ 1440 50% 129600 reload-into-ims

refresh_pattern -i \.html$ 1440 90% 129600 reload-into-ims-

refresh_pattern -i \.shtml$ 1440 90% 129600 reload-into-ims

refresh_pattern -i \.hml$ 1440 90% 129600 reload-into-ims

refresh_pattern -i \.jpg$ 1440 90% 129600 reload-into-ims

refresh_pattern -i \.png$ 1440 90% 129600 reload-into-ims

refresh_pattern -i \.gif$ 1440 90% 129600 ignore-reload

refresh_pattern -i \.bmp$ 1440 90% 129600 reload-into-ims

refresh_pattern -i \.js$ 1440 90% 129600 reload-into-ims
</pre>

<pre>ignore-reload
</pre>

该选项导致 squid 忽略请求里的任何 no-cache 指令.

所以.如果希望内容一进入 cache 就不删除,直到被主动 purge 掉为止,可以加上 ignore-reload 选项,这个我们常用在mp3,wma,wmv,gif之类.

Examples:

<pre>refresh_pattern -i \.mp3$ 1440 50% 2880 ignore-reload

refresh_pattern -i \.wmv$ 1440 50% 2880 ignore-reload

refresh_pattern -i \.rm$ 1440 50% 2880 ignore-reload

refresh_pattern -i \.swf$ 1440 50% 2880 ignore-reload

refresh_pattern -i \.mpeg$ 1440 50% 2880 ignore-reload

refresh_pattern -i \.wma$ 1440 50% 2880 ignore-reload
</pre>

<pre>ignore-no-cache
</pre>

该选项导致 Squid 强制忽略从源站而来的“Pragma: no-cache”和“Cache-control: no-cache”

<pre>ignore-private
</pre>

该选项导致 Squid 强制忽略从源站而来的“Cache-control: private”

ignore-auth：强制将一个请求认为是源站发送的带有“Cache-control: public”

<pre>ignore-auth
</pre>

该选项导致 Squid 强制将一个请求认为是源站发送的带有“Cache-control: public”

&nbsp;

**refresh_pattern percent 的计算**

resource age =对象进入cache的时间-对象的last_modified

response age =当前时间-对象进入cache的时间

LM-factor=(response age)/(resource age)

&nbsp;

举个例子,这里只考虑percent, 不考虑min 和max

例如：refresh_pattern 20%

假设源服务器上www.aaa.com/index.htm —–lastmodified 是 2007-04-10 02:00:00

squid上 proxy.aaa.com/index.htm index.htm进入cache的时间 2007-04-10 03:00:00

1）如果当前时间 2007-04-10 03:00:00

resource age =3点-2点=60分钟

response age =0分钟

index.htm还可以在cache停留的时间(resource age)*20%=12分钟

也就是说,index.htm进入cache后,可以停留12分钟,才被重新确认.

2）如果当前时间 2007-04-10 03:05:00

resource age =3点-2点=60分钟

response age =5分钟

index.htm还可以在cache停留的时间(resource age)*20%=12分钟-5=7

LM-factor=5/60=8.3%<20%

一直到2007-04-10 03:12:00 LM-factor=12/60=20% 之后,cache中的页面index.htm终于stale.

如果这时没有 index.htm 的请求,index.htm 会一直在缓存中,如果有 index.htm 请求,squid 收到该请求后,由于已经过期, squid 会向源服务器发一个 index.htm 是否有改变的请求,源服务器收到后,如果 index.htm 没有更新,squid 就不用更新缓存,直接把 缓存的内容放回给客户端,同时,重置对象进入 cache 的时间为与源服务器确认的时间,比如 2007-04-10 03:13:00,如果正好在这个后重新确认了页面.重置后,resource age 变长,相应在 cache 中存活的时间也变长.

如果有改变则把最新的 index.htm 返回给 squid,squid 收到会更新缓存,然后把新的 index.htm 返回给客户端,同时根据新页面 中的Last_Modified 和取页面的时间,重新计算 resource age,进一步计算出存活时间.

实际上,一个页面进入 cache 后,他的存活时间就确定了,即 (resource age) * 百分比,一直到被重新确认.