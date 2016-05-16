---
layout: default
title: 连接mysql时Host 'xx.xx.xx.xx' is not allowed to connect to this Mysql server解决办法
category: mysql
excerpt: 本文主要介绍Host 'xx.xx.xx.xx' is not allowed to connect to this Mysql server解决办法。
--- 
<h2>Host 'xx.xx.xx.xx' is not allowed to connect to this Mysql server解决办法</h2>
今天刚装了一个新的虚拟机，当用虚拟机里的mysql_server测试的时候yii框架报了一个错误：

	Host '192.169.0.22' is not allowed to connect to this Mysql server
	
由报错猜测是虚拟机没有权限访问mysql_server，所以解决办法就是通过授权给某个用户或者某个id上的某个用户的方式给用户授权。

	>mysql -uroot -p
	>grant all PRIVILEGES on demo.* to root identified by 'root'    
		
分析一下上面的参数：
	
	all PRIVILEGES==>所有权限    也可以给用户授权某一种权限：如select,insert,update,delete,create,drop等
	demo.*==>库名.表名           可以具体到某一张表，如demo.table1,demo.table2
	root                        被授权可使用mysql_server的用户名
	'root'                      被授权用户的密码

上面这种授权方法允许所有ip的主机上的root用户访问该mysql_server，如果只想给某台机器上的用户访问该mysql_server的权限，可以用下面的方法有针对性的授权：

	>grant all PRIVILEGES on demo.* to root@127.0.0.1 identified by 'root'
	
上面这种授权方法只允许固定ip上的root用户访问该mysql_server。

如果是远程执行的上述操作，执行下面的语句，mysql远程帐号可以立即生效。

	>flush privileges;
	
	
	---
layout: default
title:Host 'xx.xx.xx.xx' is not allowed to connect to this Mysql server解决办法
category: mysql
excerpt: 本文主要介绍Host 'xx.xx.xx.xx' is not allowed to connect to this Mysql server解决办法。
--- 