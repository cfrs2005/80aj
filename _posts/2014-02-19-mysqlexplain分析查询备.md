---
title: 140219 mysql explain分析查询备
layout: post
permalink: /2751.html
categories:
  - DataBase
tags:
  - EXPLAIN
  - mysql
  - 注解
---
<p>请原谅不是很优秀的成员的脑袋是记不住很多不是很敏感的东西。explain就是如此。</p>
<p><font color="red">新同事发来一个查询,2个子查询，1个union查询,虽然已经使用了limit,但是实际上在查询的时候还是进行了正表查询，幸亏表记录比较少才1.6W所以查询结果看上去没有太大的异常，执行没有超过1秒这类的。不是太过于执着得我就认了。</font></p>
<p>但是这种禁忌错误我还是需要去记录下来，告诫自己。在尽可能的情况下可以代码本身可以优化的尽量去做掉，不要在写sql的时候发现逻辑是如此的糟糕。</p>
<p>explain一直都在用，可是每次用的时候都会去查XX，很麻烦，网上找了片还不错的使用注解放在这里。</p>
<h3>explain分析查询</h3>
<p>使用 EXPLAIN 关键字可以模拟优化器执行SQL查询语句，从而知道MySQL是如何处理你的SQL语句的。这可以帮你分析你的查询语句或是表结构的性能瓶颈。通过explain命令可以得到:</p>
<p>– 表的读取顺序</p>
<p>– 数据读取操作的操作类型</p>
<p>– 哪些索引可以使用</p>
<p>– 哪些索引被实际使用</p>
<p>– 表之间的引用</p>
<p>– 每张表有多少行被优化器查询</p>
<p><a href="http://pic.80aj.com/2014/02/explain.jpg"><img src="http://pic.80aj.com/2014/02/explain.jpg" alt="explain" /></a></p>
<p>EXPLAIN字段：</p>
<pre>
ØTable：显示这一行的数据是关于哪张表的

Øpossible_keys：显示可能应用在这张表中的索引。如果为空，没有可能的索引。可以为相关的域从WHERE语句中选择一个合适的语句

Økey：实际使用的索引。如果为NULL，则没有使用索引。MYSQL很少会选择优化不足的索引，此时可以在SELECT语句中使用USE INDEX（index）来强制使用一个索引或者用IGNORE INDEX（index）来强制忽略索引

Økey_len：使用的索引的长度。在不损失精确性的情况下，长度越短越好

Øref：显示索引的哪一列被使用了，如果可能的话，是一个常数

Ørows：MySQL认为必须检索的用来返回请求数据的行数

Øtype：这是最重要的字段之一，显示查询使用了何种类型。从最好到最差的连接类型为system、const、eq_reg、ref、range、index和ALL

nsystem、const：可以将查询的变量转为常量.  如id=1; id为 主键或唯一键.

neq_ref：访问索引,返回某单一行的数据.(通常在联接时出现，查询使用的索引为主键或惟一键)

nref：访问索引,返回某个值的数据.(可以返回多行) 通常使用=时发生

nrange：这个连接类型使用索引返回一个范围中的行，比如使用>或<查找东西，并且该字段上建有索引时发生的情况(注:不一定好于index)

nindex：以索引的顺序进行全表扫描，优点是不用排序,缺点是还要全表扫描

nALL：全表扫描，应该尽量避免

ØExtra：关于MYSQL如何解析查询的额外信息，主要有以下几种

nusing index：只用到索引,可以避免访问表. 

nusing where：使用到where来过虑数据. 不是所有的where clause都要显示using where. 如以=方式访问索引.

nusing tmporary：用到临时表

nusing filesort：用到额外的排序. (当使用order by v1,而没用到索引时,就会使用额外的排序)

nrange checked for eache record(index map:N)：没有好的索引.

</pre>
<p>参考资料:</p>
<p>http://www.oicto.com/mysql-explain-show/</p>
