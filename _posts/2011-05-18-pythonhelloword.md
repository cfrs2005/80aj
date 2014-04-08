---
title: '110518  python hello word'
layout: post
permalink: /2093.html
categories:
  - Code
tags:
  - hello word
  - prerequistes for app engirne development are missing
  - python
---
谷歌 gae 下载 python 环境

http://code.google.com/appengine/downloads.html#Google\_App\_Engine\_SDK\_for_Python

python sdk 包

http://www.python.org/ftp/python/2.6.6/

注意事项:  
1:  
Python sdk包 如果大于 2.6 比如说 3.2 就会遇到报错

NameError: global name &#8216;execfile&#8217; is not defined

2:  
安装完2个软件以后会遇到 :

prerequistes for app engirne development are missing

找不到 python 解析器  
环境问题 配置下环境即可

右键我的电脑 ->属性->高级->环境变量  
增加 系统变量 python 你的python 系统路径  
如果不行  
path 中 增加 ;c:\python26

新建 python 项目的时候  
配置文件 app.yaml  
中 必须格式必须严格 多一个空格都会有错

正确格式

<pre>application: engineapp
version: 1
runtime: python
api_version: 1

handlers:
- url: .*
  script: helloworld.py

</pre>

错误的如下

<pre>application: engineapp
version: 1
runtime: python
api_version: 1

handlers:
- url: .*
script: helloworld.py

</pre>

&nbsp;

<pre lang="python">from google.appengine.ext import webapp
from google.appengine.ext.webapp import util


class MainHandler(webapp.RequestHandler):
    def get(self):
        self.response.out.write('Hello world!')


def main():
    application = webapp.WSGIApplication([('/', MainHandler)],
                                         debug=True)
    util.run_wsgi_app(application)


if __name__ == '__main__':
    main()

</pre>

&nbsp;