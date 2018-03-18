---
layout: post
title: Maven的安装与配置
categories: Maven
description: Maven的安装与配置
keywords: Maven, 环境, Env
---

上一讲 [为什么要在 Java 项目中使用 Maven](https://www.jianshu.com/p/b36bbf8adf8d) 中已经介绍了 Maven 的优点与功能。今天，我们来看看怎么在本地安装和配置 Maven 工具！

## 1、Maven安装

### 下载

去 [Maven 官网](https://maven.apache.org/download.cgi) 下载最新版Maven组建：

![image](http://upload-images.jianshu.io/upload_images/2946710-30a78710c37eb3cd?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解压到一个存放开发工具的目录里：

![image](http://upload-images.jianshu.io/upload_images/2946710-7fb481a544e0e646?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到这一步，安装就完成了~~
<!--more-->
## 2、配置环境变量

Windows 系统：

> 打开系统属性-环境变量，添加 M2_HOME -> 路径信息；
> 
> 在Path内添加 %M2_HOME%\bin;

Mac 系统：

打开 Terminal 输入如下指令:

> open ~/.bash_profile

添加下列两行代码并保存：

> export M2_HOME=/Library/apache-maven-3.5.2
> 
> export PATH=$PATH:$M2_HOME/bin

输入命令使bash_profile生效:
> source ~/.bash_profile

![image](http://upload-images.jianshu.io/upload_images/2946710-c907b4bbe7778e46?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

测试，在 Terminal 中输入 mvn -version 看显示是否正常！

![image](http://upload-images.jianshu.io/upload_images/2946710-c8cc307effa23750?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3、Maven配置文件

将下载的 Maven 目中 conf/settings.xml 文件复制到 %HOME%\.m2 目录下（如没有，可手动创建）！

![image](http://upload-images.jianshu.io/upload_images/2946710-640835fa0fae0452?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

用编辑器打开 settings.xml 文件，并修改下面内容：

> mirrors 可以配置下载软件包的地址，中心仓库访问压力大，镜像地址的访问成功率高！
```
     <mirror>
    	<id>nexus-aliyun</id>
    	<mirrorOf>*</mirrorOf>
    	<name>Nexus aliyun</name>
    	<url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
```
![image](http://upload-images.jianshu.io/upload_images/2946710-0e857b6c4ace7959?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 4、在 Eclipse 中集成 Maven

下载eclipse（请下载最新版本，最新版本自带m2e）

> 配置eclipse：Eclipse -> window -> Preference -> Maven -> Installations -> Add“配置安装路径”

![image](http://upload-images.jianshu.io/upload_images/2946710-49b997d9ef4bcf3f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> Eclipse -> window -> Preference -> Maven -> User Settings 指向Maven配置文件拷贝到的地址！

![image](http://upload-images.jianshu.io/upload_images/2946710-c719f098ee380e7c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
至此，Maven 的安装和配置就已经完成了，小伙伴们如果遇到什么问题可以在文章下留言交流哦~~
