---
title: 120917 phpcms dbfactory 重建链接的时候单实例引发的问题
layout: post
permalink: /2329.html
categories:
  - Code
tags:
  - bug
  - mysql_select_db
  - phpcms
  - 单实例
---
[<img src="http://www.80aj.com/wp-content/uploads/2012/09/phpcms.jpg" alt="" title="phpcms" width="397" height="125" class="aligncenter size-full wp-image-2330" />][1]

phpcms 在使用得过程中无奈的一直出现BUG 也不能全怪 phpcms 主要是加载的类库中 mysql 有 db设置选项

<pre lang="php">pc_base::load_sys_class("get_model", "model", 0);
                                                $get_db = new get_model();
                                                //var_dump($get_db);
                                                $r = $get_db->sql_query("select * from v9_news where catid in ($catid) and status=99
 and timetask!=0 order by id desc LIMIT 20");
</pre>

执行出错 db 到其他数据库去了

当程序有多mysql 加载得时候 phpcms 并没有严格的去设置 database 

有些不严谨的代码库中 加载了 mysql执行 

mysql\_select\_db(&#8220;test_db&#8221;);

但未重置得时候

phpcms/libs/classes/db_factory.class.php 

<pre lang="php">/**
         * 获取数据库操作实例
         * @param $db_name 数据库配置名称
         */
        public function get_database($db_name) {
                if(!isset($this->db_list[$db_name]) || !is_object($this->db_list[$db_name])) {
                        $this->db_list[$db_name] = $this->connect($db_name);
                }
                return $this->db_list[$db_name];
        }
</pre>

这样得 得无效 判断链接 导致 执行得时候 错库 

推荐个php代码 可查看当前所使用的数据库信息

<pre lang="php">$query="select database() AS `db`, user() AS `user`"; 
$result=mysql_query($query); 
$row = mysql_fetch_assoc($result); 
echo 'database: '.$row['db'],'<p>
  '; 
  echo 'user: '.$row['user']; 
  </pre>

 [1]: http://www.80aj.com/wp-content/uploads/2012/09/phpcms.jpg