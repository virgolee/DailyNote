---
layout: post
title: MySQL安装未响应的解决方法
categories: [MySQL]
description: 解决MySQL安装到最后一步未响应的三种方法
keywords: Mysql
---

# 解决MySQL安装到最后一步未响应的三种方法

最近公司电脑又出问题重装系统了,感觉该换电脑了╮(╯▽╰)╭.

然后在安装MySQL的时候一直卡在最后一步,各种未响应!!!

经过一番Google,Baidu后终于得到了解决.现在把方法记录一下,说不定有用呢.

## 问题:

安装MySQL卡在最后一步,未响应.

## 解决：

### 方法一

安装MySQL的时候在这一步时它默认的服务名是“MySQL” 只需要把这个名字改了就可以了。可以把默认的服务器的名称手动改为你没用过的其他名称。

### 方法二

1、卸载MySQL 

  2、删除安装目录及数据存放目录   

3、在注册表(regedit)查询mysql，全部删除   

4、在c盘查询MySQL，全部删除  ;一般是在ProgramData文件夹下（该文件是隐藏的，需要设置为显示隐藏文件）和winbdows文件夹下

5、重新安装就好了
注意的是注册表 cmd -> regedit
1.HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL 目录
2.HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL 目录
3.HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL 目录
4.HKEY_LOCAL_MACHINE\SYSTEM\CurrentControl001t\Services\MYSQL 目录
5.HKEY_LOCAL_MACHINE\SYSTEM\CurrentControl002\Services\MYSQL 目录
6.HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MYSQL 目录
7.删除C:\Documents and Settings\All Users\Application Data\MySQL 目录

### 方法三：

 **这个方法比较有用**

1.关掉未响应的那个窗口

2.然后在本地硬盘找到你自己的MySQL的安装文件夹

3.打开bin目录

4.直接运行MySQLInstanceConfig.exe(可能需要管理员身份运行)重新配置一次

5.按照你正常安装的选项去配置

这个时候你发现最后一步已经打了2个√,甚至直接装好,也有可能2个√之后又卡死

6.如果又卡死了就在回到步骤4,继续安装.
