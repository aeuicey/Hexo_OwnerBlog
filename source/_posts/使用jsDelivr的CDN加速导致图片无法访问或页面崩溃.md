---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T20:02:27.229888+08:00'
tags:
- CDN
title: 使用jsDelivr的CDN加速导致图片无法访问或页面崩溃
updated: '2025-08-27T20:02:27.634+08:00'
---
## 一、背景

  [![](https://gcore.jsdelivr.net/gh/aeuicey/Picwent/pic/20250312155536317.png)](https://gcore.jsdelivr.net/gh/aeuicey/Picwent/pic/20250312155536317.png)

一般来说，我们使用图片或者其他静态资源链接都会采用CDN加速，这样能提升我们的访问速度。比如GitHub作为图床都会使用CDN加速，因为我们访问GitHub的速度确实不敢恭维，然而有时候我们会出现Github图床外链或者其他静态资源链接使用Jsdelivr的CDN加速访问失败。

## 二、原因

  Jsdelivr国内的CDN服务被DNS污染了，被指向了Google、Twitter 和 Facebook 的 IP 地址，导致使用CDN服务加速的链接访问失败。

## 三、解决办法

  Jsdelivr国内的CDN服务被DNS污染，往往一般是cdn.jsdelivr.net被DNS污染了，而其他代替的地址没有被污染，比如fastly.jsdelivr.net、gcore.jsdelivr.net等。这时候我们就可以批量把图片或者其他静态资源链接中的cdn.jsdelivr.net替换为别的可用的地址（下面自己选一个可用的），等官方修复回去后再替换回去就行了。

比如：

**无CDN加速**

`https://raw.githubusercontent.com/SmallGawk/blog-image/master/image/test.png`

**Jsdelivr的DNS被污染**

`https://cdn.jsdelivr.net/gh/SmallGawk/blog-image/image/test.png`

**Jsdelivr替换后的**

`https://gcore.jsdelivr.net/gh/SmallGawk/blog-image/image/test.png`

## 四、可用（代替）地址

`fastly.jsdelivr.net`

`gcore.jsdelivr.net`

`testingcf.jsdelivr.net`

`test1.jsdelivr.net`

## 五、总结

本文简单讲述了jsDelivr的CDN加速被污染的原因以及解决办法

> source: https://blog.csdn.net/weixin\_45260582/article/details/129272400
>
