---
title: PHP库
layout: page
ratings_users:
  - 0
ratings_score:
  - 0
ratings_average:
  - 0
views:
  - 3
duoshuo_thread_id:
  - 1280248249638191398
---
<pre>2014-1-14 更新:
</pre>

### CSS,JS压缩

Web性能优化最佳实践中最重要的一条是减少HTTP请求，它也是YSlow中比重最大的一条规则。减少HTTP请求的方案主要有合并JavaScript和CSS文件、CSS Sprites、图像映射（Image Map）和使用Data URI来编码图片。CSS Sprites和图像映射现在已经随处可见了，但由于IE6和IE7不支持Data URI以及性能问题，这项技术尚未大量使用。目前大部分网页中的JavaScript和CSS文件数量和开发时一致，少量的网页会根据实际情况采取本地合并，这些合并中相当多的是有选择地手动完成，每次新的合并都需要重新在本地完成并上传到服务器，比较的随意和繁琐，同样文件的压缩也有类似的情况。而利用服务端的合并和压缩，我们就可以按照开发的逻辑尽可能让文件的颗粒度变小，利用网页中URL的规则来自动实现文件的合并和压缩，这会相当的灵活和高效。

1.  <a title="Combo Handler" href="http://www.yuiblog.com/blog/2008/07/16/combohandler/" target="_blank">Combo Handler </a> – 2008年7月YUI Team宣布在YAHOO! CDN上对YUI JavaScript组件提供Combo Handler服务。
2.  <a title="Minify" href="https://code.google.com/p/minify/" target="_blank">Minify</a> – PHP的开源项目叫Minify，它可以合并、精简、Gzip压缩和缓存JavaScript和CSS文件。

### 图表库

下面的类库可以让你很简的创建复杂的图表和图片。当然，它们需要GD库的支持。

<div>
  <ol>
    <li>
      <a title="pChart" href="http://pchart.sourceforge.net/" target="_blank">pChart</a> – 一个可以创建统计图的库。
    </li>
    <li>
      <a title="Libchart" href="http://naku.dohcrew.com/libchart/pages/introduction/" target="_blank">Libchart</a> – 这也是一个简单的统计图库。
    </li>
    <li>
      <a title="JpGraph" href="http://www.aditus.nu/jpgraph/" target="_blank">JpGraph</a> – 一个面向对象的图片创建类。
    </li>
    <li>
      <a title="Open Flash Chart" href="http://teethgrinder.co.uk/open-flash-chart/" target="_blank">Open Flash Chart</a> – 这是一个基于Flash的统计图。
    </li>
  </ol>
</div>

### RSS 解析

解释RSS并是一件很单调的事情，不过幸好你有下面的类库可以帮助你方便地读取RSS的Feed。

1.  <a title="MagpieRSS" href="http://magpierss.sourceforge.net/" target="_blank">MagpieRSS</a> – 开源的PHP版RSS解析器，据说功能强大，未验证。
2.  <a title="SimplePie" href="http://simplepie.org/" target="_blank">SimplePie</a> – 这是一个非常快速，而且易用的RSS和Atom 解析库。

### 缩略图生成

1.  <a title=" phpThumb" href="http://phpthumb.sourceforge.net/" target="_blank">phpThumb</a> – 功能很强大，如何强大还是自己去体会吧。

### 支付

你的网站需要处理支付方面的事情？需要一个和支付网关的程序？下面这个程序可以帮到你。

1.  <a title="PHP Payment Library" href="http://www.phpfour.com/blog/2009/02/php-payment-gateway-library-for-paypal-authorizenet-and-2checkout/" target="_blank">PHP Payment Library</a> – 支持Paypal, Authorize.net 和2Checkout (2CO)

### OpenID

1.  <a title="PHP-OpenID" href="http://www.openidenabled.com/php-openid/" target="_blank">PHP-OpenID</a> – 支持OpenID的一个PHP库。OpenID是帮助你使用相同的用户名和口令登录不同的网站的一种解决方案。如果你对OpenID不熟悉的话，你可以到这里看看：<http://openid.net.cn/>

### 数据为抽象/对象关系映射ORM

1.  <a title="ADOdb" href="http://adodb.sourceforge.net/" target="_blank">ADOdb</a> – 数据库抽象
2.  <a title="Doctrine" href="http://www.doctrine-project.org/" target="_blank">Doctrine</a> – 对象关系映射Object relational mapper (ORM) ，需要 PHP 5.2.3+ 版本，一个非常强大的database abstraction layer (DBAL).
3.  <a title="Propel" href="http://propel.phpdb.org/trac/" target="_blank">Propel</a> – 对象关系映射框架- PHP5
4.  <a title="Outlet" href="http://www.outlet-orm.org/site/" target="_blank">Outlet</a> – 也是关于对象关系映射的一个工具。

注：对象关系映射（Object Relational Mapping，简称ORM）是一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。 简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系数据库中。本质上就是将数据从一种形式转换到另外一种形式。 这也同时暗示者额外的执行开销；然而，如果ORM作为一种中间件实现，则会有很多机会做优化，而这些在手写的持久层并不存在。 更重要的是用于控制转换的元数据需要提供和管理；但是同样，这些花费要比维护手写的方案要少；而且就算是遵守ODMG规范的对象数据库依然需要类级别的元数据。

### PDF 生成器

1.  <a title="FPDF" href="http://www.fpdf.org/" target="_blank">FPDF</a> – 这量一个可以让你生成PDF的纯PHP类库。

### Excel 相关

你的站点需要生成Excel？没有问题，下面这两个类库可以让你轻松做到这一点。

<div id="psum">
  <ol>
    <li>
      <a title="php-excel" href="http://code.google.com/p/php-excel/" target="_blank">php-excel</a> – 这是一个非常简单的Excel文件生成类。
    </li>
    <li>
      <a title="PHP Excel Reader" href="http://code.google.com/p/php-excel-reader/" target="_blank">PHP Excel Reader</a> – 可以解析并读取XLS文件中的数据。
    </li>
  </ol>
</div>

### E-Mail 相关 {#psum}

不喜欢PHP的mail函数？觉得不够强大？下面的PHP邮件相关的库绝对不会让你失望。

<div>
  <ol>
    <li>
      <a title="Swift Mailer" href="http://swiftmailer.org/" target="_blank">Swift Mailer</a> – 免费的超多功能的PHP邮件库。
    </li>
    <li>
      <a title="PHPMailer" href="http://phpmailer.codeworxtech.com/" target="_blank">PHPMailer </a>- 超强大的邮件发送类。
    </li>
  </ol>
  
  <h3>
    单元测试
  </h3>
  
  <p>
    如果你在使用测试驱动的方法开发你的程序，下面的类库和框架绝你能帮助你的开发。
  </p>
</div>

1.  <a title="SimpleTest" href="http://www.simpletest.org/" target="_blank">SimpleTest</a> – 一个PHP的单元测试和网页测试的框架。
2.  <a title="PHPUnit" href="http://www.phpunit.de/" target="_blank">PHPUnit</a> – 来自xUnit 家族，提供一个框架可以让你方便地进行单元测试的案例开发。并可非常容易地分析其测试结果。

### 相关资料:

http://coolshell.cn/articles/200.html