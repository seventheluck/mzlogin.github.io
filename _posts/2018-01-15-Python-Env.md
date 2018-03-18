---
layout: post
title: Python环境安装
categories: Python
description: Python环境安装
keywords: Python, 开发环境
---

# 1、Python解释器的安装

目前，Python有两大版本：2.x版、3.x版，本文以目前使用比较普遍的3.x版本为例，请务必在看完所有安装方法后再动手尝试，万一后面还有更好的方法呢，哈哈哈😁。

## Mac 系统

使用Mac系统的同学需要注意，Mac系统会自带一个2.x的版本，此处不建议卸载自带版本，因为操作起来比较麻烦并且容易为未来埋下隐患，我们只需要直接安装3.x版本即可。安装3.xPython有两个方法：
<!--more-->
1、官网下载

从[Python官网](https://www.python.org/)直接下载，双击文件安装。

2、通过Homebrew安装

首先通过Terminal终端输入如下命令（可参考[Homebrew](https://brew.sh/)）：

> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

然后在Terminal终端输入如下命令：

> brew install python3

## Windows系统

从[Python官网](https://www.python.org/)直接下载，双击文件安装。

**需要注意的是，为了避免安装后环境变量未生效，在安装界面一定要勾选 Add Python3.x to PATH，切记！**

## Linux系统

Ubuntu上：

> $ sudo apt-get install python3.x

其他Linux系统可以使用包管理器。

## 神器Anaconda

前面我们已经介绍了Python解释器的安装方法，接下来介绍另外一种完全不同的上手Python的方法，这就是Anaconda，它有什么优点值得我们单独介绍？

第一，Anaconda是一个Python包管理器和环境管理器，它包含了非常多的第三方常用模块，你可以很方便的通过Anaconda安装和管理第三方的模块，省去了pip这个依赖包那个依赖包的麻烦。

第二，Python有一个很大的问题，版本多且很多第三方模块支持的不是很好，有的适用于2.x，有的适用于3.x，还有的要3.5.x以下版本才行，有时候真的能被整崩溃。

Anaconda安装：

官网下载地址：[Anaconda](https://www.anaconda.com/download/#macos)

Anaconda同样有两个版本对应Python2.x和3.x，如果没特殊需求，请直接安装3.x版本。安装时按照提示即可，适用默认设置即可。在安装时Anaconda会自动设置环境变量。Linux和Mac系统会将设置写到~/.bashrc文件，Windows系统会将设置写到到系统变量PATH。安装完成后可以通过在Terminal终端中输入如下命令查看版本是否正确：

> conda --version

> python --version

# 2、Python IDE推荐

## Pycharm

首选Pycharm，功能强大非常好用，有钱的可以购买专业版，学生可以申请学生版，没钱的可以使用免费的社区版。

## Sublime Text

仅次于Pycharm，优点是可以免费使用。

# Jupyter Notebook

Jupyter Notebook是一个交互式笔记本，Jupyter不算是Python的IDE，但是用起来非常顺手，暂且算到这里面吧。Jupyter分为在线版本和本地版本。

[在线Jupyter](https://try.jupyter.org/)使用的人很多，经常打不开，所以就不指望用了。

现在推荐大家使用本地版，上面介绍了Anaconda，如果安装了Anaconda的话，打开Anaconda就能看到下面这个界面，红圈圈出来的这个就是Jupyter，如果显示是Install，那就直接Install，如果是Lunch，那就直接点击Lunch就行。

![image](http://upload-images.jianshu.io/upload_images/2946710-d131e80bab90ae64?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

对于没有安装Anaconda的同学来说，可以在Terminal终端输入如下命令安装：

> python -m pip install jupyter

运行方法：

> jupyter notebook

打开以后可以看到这个界面：

![image](http://upload-images.jianshu.io/upload_images/2946710-ad490ea333af75c9?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击 New - Python3：

![image](http://upload-images.jianshu.io/upload_images/2946710-06b48640f83f5d90?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在下图红框内输入Python代码即可：

![image](http://upload-images.jianshu.io/upload_images/2946710-edcbd7f12c3ffd5a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](http://upload-images.jianshu.io/upload_images/2946710-3fac612999e03c99?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击红圈内的按钮：

![image](http://upload-images.jianshu.io/upload_images/2946710-0324a336d700f76f?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到执行结果：

![image](http://upload-images.jianshu.io/upload_images/2946710-4a16efb2cde687c5?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Jupyter的功能非常强大，大家可以自己探索。

以上就是Python环境搭建的说明，谢谢！
