---
layout: default
title: centos中yum资源地址
category: Linux
excerpt: 本文主要介绍centos系统中使用yum安装常用软件时用得到的资源地址
---
<h2>centos yum资源地址</h2>

yum是centos中安装软件的一个利器，只需要一条简单的install命令就可以搞定软件下载、安装和依赖。yum的工作原理就是去.repos文件中指向的软件仓库中获取相应的软件以及其该软件相关的依赖，但是很多软件并不在centos自带的软件仓库中，所以当我们使用yum去查找的时候会找不到软件，今天整理了一下比较好用的yum资源仓库，以后再使用yum安装软件的时候就不用到处去找yum源了。

<h3>yum源</h3>
**epel源**  
\#用于RHEL5系列

	wget http://download.fedoraproject.org/pub/epel/5/i386/epel-release-5-4.noarch.rpm
	rpm -ivh epel-release-5-4.noarch.rpm
	
\#用于RHEL6系列

	wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-5.noarch.rpm
	rpm -ivh epel-release-6-5.noarch.rpm
	
\#适用于RHEL7

	rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm

有时安装完epel的源，运行yum会报错：Cannot retrieve metalink for repository：epel.Please verify its path and try again.
<p class="red">解决办法：将epel.repo文件中的mirrorlist路径注释掉，将baseurl前的注释取消</p>

**rpmforge源(centos官方推荐软件仓库)**

1、首先安装priorities插件

	yum install yum-priorities
	确认/etc/yum/pluginconf.d/priorities.conf中包含：
	[main]
	enabled=1
	
2、现在可以手动编辑/etc/yum.repos.d/目录中后缀为.repos的文件设置软件仓库的优先级了。
priority=N(N=1~99),1的优先级最高，99最低

3、安装rpmforge的软件仓库  
a.安装DAG的PGP Key
**RPM-GPG-KEY.dag.txt:包含一段PGP公钥，The following public key can be used to verify RPM packages downloaded from  http://dag.wieers.com/apt/  using 'rpm -K'
if you have the GNU GPG package.
意思是这段公钥可用用来认证从http://dag.wieers.com/apt/下载的RPM包**
	
	rpm --import http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt
	
b.获取rpforge的rpm安装包
\#用于RHEL7系列

	wget http://apt.sw.be/redhat/el7/en/x86_64/rpmforge/RPMS/rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm
	
c.验证下载包的完整性

	rpm -K rpmforge-release-0.3.6-1.el5.rf.*.rpm
	
d.安装rpm包

	rpm -ivh rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm
	
e.更改rpmforge的优先级
	
	priority=N;
	
接下来，就可以使用rpmforge的yum软件仓库了。

<h3>webtatic源</h3>
\#用于RHEL7系列

	rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

<h3>mysql源</h3>
\#用于RHEL7系列

	rpm -Uvh https://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

<h3>Remi源</h3>
Remi 源包含了众多软件, 它的更新速度很快. 很多新版本的软件都能第一时间在这里找到.进入 Remi 官网, 找到 Maintained Enterprise Linux (RHEL / CentOS / Other clones) 项，根据系统架构选择相应 release 文件

	rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

<h3>RPMforge源</h3>

	rpm -ivh http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm

<h3>Nginx源</h3>

进入 Nginx 官网 , 点右侧的 download 链接, 拉到最下面找到 Pre-Built Packages 项. 点mainline version 版本的链接. 根据提示编辑 repo 文件的内容, 具体操作如下.
在 yum repo 目录创建新的 nginx.repo 文件
 
	vi /etc/yum.repos.d/nginx.repo

	[nginx]
	name=nginx repo
	baseurl=http://nginx.org/packages/mainline/centos/6/$basearch/
	gpgcheck=0
	enabled=1
	
保存退出