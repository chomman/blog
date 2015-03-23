---
id: 1419
title: Mysql Function 관련 명령어
author: 정태현
layout: post
guid: http://monggu.com/?p=1419
permalink: /mysql-function-%ea%b4%80%eb%a0%a8-%eb%aa%85%eb%a0%b9%ec%96%b4/
exclude:
  - 
url:
  - 
hdimage:
  - 
slide_template:
  - default
custom_sidebar:
  - Default
post_video_type:
  - youtube
categories:
  - DB
  - Programming
tags:
  - function
  - mysql
  - procedure
  - trigger
---
Mysql 에서 덤프를 뜰 때 function은 포함되지 않는 문제가 생겨 찾아보았다.

<pre class="lang:mysql decode:true">mysql&gt;
mysql&gt;
mysql&gt; DELIMITER //
mysql&gt;
mysql&gt; CREATE FUNCTION myFunction (item_sum DECIMAL(10,2))
    -&gt; RETURNS DECIMAL(10,1)
    -&gt; BEGIN
    -&gt;
    -&gt;
    -&gt; RETURN ROUND(item_sum,1);
    -&gt;
    -&gt; END
    -&gt; //
Query OK, 0 rows affected (0.02 sec)

mysql&gt; DELIMITER ;
mysql&gt;
mysql&gt; select myFunction(123.12);
+--------------------+
| myFunction(123.12) |
+--------------------+
|              123.1 |
+--------------------+
1 row in set (0.00 sec)

mysql&gt;
mysql&gt;
mysql&gt;
mysql&gt; SHOW CREATE FUNCTION test.myFunction\G
*************************** 1. row ***************************
       Function: myFunction
       sql_mode:
Create Function: CREATE DEFINER=`root`@`localhost` FUNCTION `myFunction`(item_sum DECIMAL(10,2)) RETURNS decimal(10,1)
BEGIN
RETURN ROUND(item_sum,1);
END
1 row in set (0.00 sec)

mysql&gt;
mysql&gt; drop function myFunction;
Query OK, 0 rows affected (0.00 sec)</pre>

mysqldump는 기본적으로 모든 트리거는 백업하고, stored procedures/functions은 백업하지 않는다.

&#8211;routines &#8211; FALSE by default  
&#8211;trigger &#8211; TRUE by default

즉, stored procedure를 백업할려면, &#8211;routines 옵션을 주어야 한다.

백업

mysqldump &#8211;routines &#8211;no-create-info &#8211;no-data &#8211;no-create-db &#8211;skip-opt <database> > outputfile.sql  
복원

mysql <database> < outputfile.sql



<!-- SEO Ultimate (http://www.seodesignsolutions.com/wordpress-seo/) - Code Inserter module -->

  
  
<ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-4058194403762977" data-ad-slot="4726363844"></ins>  
<!-- /SEO Ultimate -->