---
title: 110712 linux上配置unixODBC和FreeTDS访问MSSQLServer
author: 张 清月
layout: post
permalink: /2191.html
bot_views:
  - 224
duoshuo_thread_id:
  - 1280248249638191293
views:
  - 1
categories:
  - DataBase
tags:
  - FreeTDS
  - LINUX
  - unixODBC
  - 访问MSSQLServer
  - 配置
---
一, 安装 unixODBC

下载安装包. 在 RedHat 安装光盘上就有  
unixODBC-2.2.11-1.RHEL4.1.i386.rpm  
unixODBC-devel-2.2.11-1.RHEL4.1.i386.rpm  
unixODBC-kde-2.2.11-1.RHEL4.1.i386.rpm

安装  
rpm -Uvh unixODBC-2.2.11-1.RHEL4.1.i386.rpm  
rpm -Uvh unixODBC-devel-2.2.11-1.RHEL4.1.i386.rpm  
如果安装中提示有对其它安装包的依赖,则按照提示先安装  
哪些包.

或者从源码安装 unixODBC  
下载源码集  
unixODBC-2.2.11.tar.gz  
\# tar xzf unixODBC-2.2.11.tar.gz  
\# cd unixODBC-2.2.11  
\# ./configure  
\# make  
\# make install

./configure 的时候也有可能提示找不到某些依赖库.  
下载这些依赖库的源码,编译,安装.

rpm 安装和源码编译安装的差别在于配置文件 odbc.ini, odbcinst.ini  
的位置不同. 前者为 /etc , 后者为 /usr/local/etc

二, 安装 FreeTDS

unixODBC 提供了Linux 对ODBC 的支持,但它只是一个 ODBC的管理器, 要连接  
实际的数据库还得提供这种数据库的 ODBC 驱动.

FreeTDS就是Linux 下 用于连接MS SQL Server 和 Sybase 的免费ODBC 驱动  
注意, 必须先装 unixODBC, 再装 freetds

freetds-0.64 是目前的最新稳定版.  
下载源码包 freetds-stable.tgz  
\# tar xzf freetds-stable.tgz  
\# ./configure &#8211;with-unixodbc=/usr/local &#8211;with-tdsver=8.0  
\# make  
\# su  
\# make install  
将安装到 /usr/local 下

如果 unixODBC是源码安装, 则  
&#8211;with-unixodbc=/usr/local  
如果 unixODBC是rpm安装, 则  
不需要该选项

三, 配置 unixODBC 和 FreeTDS

3.1 向unixODBC 登记 FreeTDS 驱动  
修改 /etc/odbcinst.ini (或者/usr/local/etc/odbcinst.ini)  
在文件中添加  
=========================== /etc/odbcinst.ini  ======================  
\# Driver from FreeTDS package  
\# setup from FreeTDS package  
[FREETDS]  
Description     = ODBC of FreeTDS for MS SQL 2000  
Driver          = /usr/local/lib/libtdsodbc.so  
Setup           = /usr/local/lib/libtds.so  
FileUsage       = 1

===================================================================

3.2  在 FreeTDS 的配置文件中添加指向具体数据库的访问信息  
修改 /usr/local/etc/freetds.conf  
在末尾添加如下内容. 该配置文件中原有的内容请仔细阅读, 是不错的教材  
===================================================================  
[MYSQLSERVER]  
host = 192.168.0.5    ; MS SQL Server 的 IP 或者域名  
port = 1433  
tds version = 8.0  
client charset = UTF-8  ; 客户端软件可识别的字符集.  
===================================================================  
注意, client charset 必需大于或等于服务端数据库使用的字符集.  
例如,服务端数据库是 MS SQL Server 2000, 字符集是 GB2312.  
那么 client charset 可以设置为 GB2312(等于), GB18030(大于),UTF-8(大于)  
但不能设为ISO-8859-1(小于), Shift_JIS(不等于).  
由于 UTF-8 是所由字符集的超集,因此设置为 UTF-8 总是可行的.  
此外, FreeTDS的client charset不能设置为 UTF16. 这时目前该软件设计的局限,  
其官方网站称,在未来版本中可能会增加对client charset UTF16的支持.

3.3  修改 /etc/odbc.ini (如果odbc是从源码安装,则 /usr/local/etc/odbc.ini)  
添加DSN.  
=========================== /etc/odbc.ini  ======================  
[ODBC Data Sources]  
TEST1dsn= My first Test DSN  
TEST2dsn= My second Test DSN

[TEST1dsn]        ; DSN 名  
Driver          = /usr/local/lib/libtdsodbc.so  
Description     = My First Test DSN  
Trace           = No  
Servername      = MYSQLSERVER     ;在 freetds.conf中定义  
Database        = MYTESTDB              ;库名

[TEST2dsn]  
Driver          = /usr/local/lib/libtdsodbc.so  
Description     = My Second Test DSN  
Trace           = No  
Server          = 192.168.0.5     ; 可以直接写数据库服务器的访问信息  
Database        = MyTESTDB  
Port            = 1433  
TDS_Version     = 8.0

[Default]  
Driver          = /usr/local/freetds/lib/libtdsodbc.so  
===================================================================

注意:  
用 unixODBC 通过 freeTDS 访问 MS SQL Server 有两种配置方式.

(1)一种是将服务器信息写在 freeTDS 的配置文件 $PREFIX/etc/freetds.conf 中,  
而 /etc/odbc.ini 中使用 Servername 来指向 freetds.conf 中设定的 DSN.  
如上例中的 [TEST1dsn]  
(2).另一种方式是将服务器信息也一并写在 /etc/odbc.ini 中. 如上例中的 [TEST2dsn].  
注意,关键字有所不同.  例如, freetds.conf 中的 tds version 在  
/etc/odbc.ini 中为 TDS_Version.

方式(2)相对简单,但只有少数几个关键字可以控制freetds,至于freetds的  
其它特征则使用freetds的缺省配置.

方式(1)虽然复杂一些,但对freetds可进行更细致的控制,例如可指定客户端  
的字符集.

推荐使用方式(1)进行配置.

四, 访问数据库:

无论是用客户端软件,还是编程访问数据库,通常要提供三个参数.  
DSN, UserName, Password.  
以本文示例来说,  
DSN =  TEST1dsn 或 TEST2dsn  
UserName = somename,  
Password = somepasswd,

就意味着访问位于 192.168.0.5 的 MS SQL Server 库 MYTESTDB. 查询结果  
的字符集为 UTF-8.

unixODBC 提供的一个通用的 GUI 数据库连接客户端为 DataManager.

五, 关于字符集:

FreeTDS能够自动识别服务器端的charset. 因此 FreeTDS 需要用户设定客户端的  
charset. 这也就是客户端应用程序期待从FreeTDS获得的数据所应该使用的charset.  
一旦client charset设定, FreeTDS将实现从 server charset <&#8211;> client charset  
的转换.

如果有两个客户应用程序都要访问同一个 MS SQLServer, 但很不幸,这两个客户程序所  
接受的字符集分别是 UTF-8 和 GB2312. 那么解决的办法是在FreeTDS.conf中设置  
两组DataSource,它们的服务器设置相同,但client charset分别设为 UTF-8和GB2312. 在  
odbc.ini中也设置两组不同的DSN 分别指向这两组DataSource. 而最终两个客户程序  
各自使用与之相应的DSN即可.

<span style="color: #ff0000;">六, freetds 链接 sqlserver 测试</span>

/usr/local/freetds/bin/tsql -S Server2005 -U game -P test.Com -H 192.168.1.1 -p 1433

如果遇到乱码 请尝试

freetds etc 下 执行

export LANG=zh_CN.GB18030

&nbsp;

<span style="color: #ff0000;">七, odbc使用freetds dsn 链接sqlserver</span>

<span style="color: #ff0000;">odbc.ini</span>

[game]

Servername      = Server2005   [<span style="color: #ff0000;">此为freetds配置的dsn</span>]  
Driver          = /usr/local/lib/libtdsodbc.so  
Description     = SQLSERVER  
Database        = testgame  
#UserName        =  
#Password        =  
#Port            = 1433  
Fileusage = 1

/usr/local/unixODBC/bin/isql -v game game 123123