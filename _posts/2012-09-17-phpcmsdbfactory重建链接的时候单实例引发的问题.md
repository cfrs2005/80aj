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
 phpcms 在使用得过程中无奈的一直出现BUG 也不能全怪 phpcms 主要是加载的类库中 mysql 有 db设置选项 pc\_base::load\_sys\_class("get\_model", "model", 0); $get\_db = new get\_model(); //var\_dump($get\_db); $r = $get\_db->sql\_query("select \* from v9\_news where catid in ($catid) and status=99 and timetask!=0 order by id desc LIMIT 20"); 执行出错 db 到其他数据库去了 当程序有多mysql 加载得时候 phpcms 并没有严格的去设置 database 有些不严谨的代码库中 加载了 mysql执行 mysql\_select\_db(&#8220;test\_db&#8221;); 但未重置得时候 phpcms/libs/classes/db\_factory.class.php /\*\* \* 获取数据库操作实例 \* @param $db\_name 数据库配置名称 \*/ public function get\_database($db\_name) { if(!isset($this->db\_list[$db\_name]) || !is\_object($this->db\_list[$db\_name])) { $this->db\_list[$db\_name] = $this->connect($db\_name); } return $this->db\_list[$db\_name]; } 这样得 得无效 判断链接 导致 执行得时候 错库 推荐个php代码 可查看当前所使用的数据库信息 $query="select database() AS \`db\`, user() AS \`user\`"; $result=mysql\_query($query); $row = mysql\_fetch_assoc($result); echo 'database: '.$row['db'],''; echo 'user: '.$row['user'];