---
layout: default
title: centos中使用mailx发送邮件
category: linux
excerpt: 本文将介绍一下如何在centos中借助mailx在命令行发送邮件
---
<h2>centos中使用mailx发送邮件</h2>

一直觉得用命令行是件很酷的事情，但是肿么用命令行发邮件呢？下面介绍一个很实用的软件，可以在命令行中发送邮件。

下面我们介绍两种使用mailx发送邮件的方法：

1、命令行发送

	> mailx -s "Subject" linux@gmail.com	   // Subject是指邮件的标题
	> mail body...
	> ctrl+d   // 会将邮件发出
	
2、将文件内容作为邮件体

下面的方法可以把一个文件的内容作为邮件内容发出：

	> mail -s "Subject" linux@gmail.com < demo.c

**注：1、mailx是一个软件，可使用yum安装。2、gmail会将这种方法发送的邮件放到垃圾邮件箱中。。。。可能是因为谷歌邮箱不能匹配邮件发送方。**