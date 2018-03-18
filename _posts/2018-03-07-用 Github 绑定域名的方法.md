---
layout: post
title: 用 Github 绑定域名的方法
categories: Github
description: 用 Github 绑定域名的方法
keywords: Github, Domain, 域名
---
今天自己在为 Github Pages 绑定域名的时候，顺道在网上看了很多教程，发现写的都很不清楚，不详细！于是呢，我就写下了这篇文章，希望能让看到文章的人搞清楚自己每一步都在干什么！

## 1、为 Github Pages 仓库添加 CNAME 文件

记住在你的 Github Pages 仓库根目录下添加 CNAME 文件，文件名就叫"CNAME"，文件内容就是你希望别人在浏览器输入的域名（也就是你想绑定的那个域名，也就是你花钱买来的那个个性化域名），例如：

> www.abc.com

![CNAME 文件](http://upload-images.jianshu.io/upload_images/2946710-3b08f6388a5ddcd7?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!--more-->
## 2、在 DNSPod 添加域名记录

可参考 --> [DNSPod的帮助文档](https://www.dnspod.cn/Support)

首先，没注册的需要自己先在 DNSPod 中注册一个用户，免费的，不用担心哦！

注册登录后，进入域名解析-添加记录，建议加入三条记录（如下图）注意“主机记录”、“记录类型”、“记录值”不要错：

![域名解析-添加记录](http://upload-images.jianshu.io/upload_images/2946710-bf577c5e41033f5a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 1、Github服务器地址：
> 
> 192.30.252.153
> 
> 192.30.252.154
> 
> 2、你个人主页的实际域名：
> 
> username.github.io

## 3、修改注册域名的DNS服务

以 Godaddy 为例，进入 DNS Management 页面，

![DNS Management 页面](http://upload-images.jianshu.io/upload_images/2946710-2688436dddf3bd58?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Add Nameserver](http://upload-images.jianshu.io/upload_images/2946710-8ce15d69f8f0146d?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 为 Nameserver 添加下面两个地址：
> 
> f1g1ns1.dnspod.net
> 
> f1g1ns2.dnspod.net

到此，所有配置就都已经完成，大家等五分钟左右（最差的情况下不超过72小时）就可以尝试用自己的个性域名登录Github博客了！
