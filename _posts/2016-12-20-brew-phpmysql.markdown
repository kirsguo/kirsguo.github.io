---
layout:     post
title:      "mac下安装php与MySQL"
subtitle:   " \"Hello World, Hello Blog\""
date:       2016-12-20 12:00:00
author:     "Kirsguo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
- Mac软件
---

> “Yeah It's on. ”


# 前言
我在Mac OS X Yosemite下apache **php**, **mysql**配置中写过利用系统自带的Apache与PHP配置 但这次是在**brew**下安装以及重装mysql出现的问题

---

# 正文

## 1. homebrew

[homebrew](http://brew.sh)是mac下的一个包安装管理工具，使用非常简单方便。

### 1.1 安装homebrew

在终端中执行：

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

这样就安装好homebrew了。

安装命令行软件

如安装wget，则执行：

`brew install wget`<br>
其它具体的使用方法可自行翻阅 官网（中文）。

另外介绍一下**homebrew-cask**是**homebrew**的一个扩展，用于安装图形界面mac程序，如google chrome、QQ等等。

### 1.2 安装homebrew-cask

`brew install caskroom/cask/brew-cask`

### 1.3 使用homebrew-cask

`brew cask install google-chrome`

具体的功能请翻阅官网。

## 2 LaunchRocket&&Adminer

### 2.1 launchrocket

LaunchRocket是管理homebrew所安装应用的一个管理器，它在系统设置中。 安装命令：

`brew cask install launchrocket`

（主要是为了集中管理Apache 、PHP、MySQL很好的管理器可以省略很多终端代码 ，各种数据库也能用上启动起来方便。）

### 2.2 adminer

adminer是用php写的一个数据库管理工具，可以管理 MySQL, PostgreSQL, SQLite, MS SQL, Oracle, MongoDB等类型数据库，而且还是单文件，安装部署非常方便，支持多种语言。

`rew  install adminer`
## 3 安装Apache PHP 

**因为apache和php不在默认的仓库里，所以我们要先添加其所在的仓库。**

`brew tap homebrew/apache`

`brew tap homebrew/php`

之后就是正常的安装了，安装过程homebrew会为你自行处理各种依赖。

`brew install httpd24`

`brew install php70`

**注意**：apache在homebrew中的名字为httpd。 这些都可以指定安装的版本，这里我安装apache2.4，php7.0  以下的路径说明都是以这个为基准，请自行修改为你所下载的版本。

## 4 配置Apache

配置文件路径为/usr/local/etc/apache2/2.4/httpd.conf，以下的配置都需要在相应的地方修改。

### 4.1 添加php模块
 
`====php module====`

`LoadModule php7_module /usr/local/Cellar/php70/7.0.8/libexec/apache2/libphp7.so`

`<IfModule mod_php7.c>`

`AddType application/x-httpd-php .php`

`AddType application/x-httpd-php-source .phps`

`<IfModule mod_dir.c>`

`DirectoryIndex index.html index.php`

`</IfModule>`

`</IfModule>`

### 4.2 修改监听端口 
默认的端口为8080，我们改为80：

`Listen 80`
### 4.3 修改root根目录

`DocumentRoot "/Users/kirs/Sites"`

`<Directory "/Users/kirs/Sites">`

(本地网站根目录，就是放置你项目的php或html的地方)

## 5 MySQL安装（重装）

如果之前安装过MySQL需要卸载重装，终端执行：

`sudo rm /usr/local/mysql`

`sudo rm -rf /usr/local/var/mysql`

`sudo rm -rf /usr/local/mysql*`

`sudo rm -rf /Library/StartupItems/MySQLCOM`

`sudo rm -rf /Library/PreferencePanes/My*`

`sudo rm -rf /Library/Receipts/mysql*`

`sudo rm -rf /Library/Receipts/MySQL*`

`sudo rm -rf /var/db/receipts/com.mysql.*`

**一定要确保这些都做过！！！这是我找的最全版本 要不然就是坑！Mac是没有卸载MySQL的！只能这样**

### 5.1 安装

`brew install mysql`

成功后

`mysql -uroot`

### 5.2 使用mysql的配置脚本：

/usr/local/opt/mysql/bin/mysql_secure_installation
启动这个脚本后，即可根据如下命令提示进行初始化设置（只留关键部分）

Enter current password for root (enter for none): //输入现行root密码，因为初次使用，所以直接回车

Set root password? [Y/n] Y //是否设置root密码

Remove anonymous users? [Y/n] Y //是否删除匿名用户

Disallow root login remotely? [Y/n] Y //是否禁止远程登录

Remove test database and access to it? [Y/n] Y //删除测试数据库，并登录

Reload privilege tables now? [Y/n] Y//重新载入权限表
配置结束，再次登录需终端执行：

`mysql -u root -p`
会有密码提示输入即可

---
# 后记
各版本可能会有所不同，出现问题欢迎邮件联系我，一起讨论研究


