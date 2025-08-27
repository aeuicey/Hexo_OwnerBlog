---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:19:21.185209+08:00'
tags:
- 激活Windows
title: TSforge 激活Windows
updated: '2025-08-27T19:19:22.503+08:00'
---
[![](https://i.blogs.es/1e6d84/win11-hero/1366_2000.jpeg)](https://i.blogs.es/1e6d84/win11-hero/1366_2000.jpeg)

## **0. 简介**

长期致力于 Windows 10/11 和 Microsoft Office 产品激活的 Massgrave 团队日前宣布新激活方式：TSforge 激活，该激活方式可以激活 Windows 和 Office 所有现代版本。

最新推出的 MAS 3.0 版更新已经集成新的激活方式，MAS 团队称这是有史以来最强大也是影响最为深远的激活漏洞，可以绕过微软激活保护系统的各种措施。

## **1. TSForge 能够激活的 Windows 包括：**

Windows 11 所有版本

Windows 10 所有版本

Windows 8.1 所有版本

Windows 7 所有版本

Windows Server 2008 R2\~Windows Server 2025 所有版本

## **2. TSForge 支持的 Office 版本包括：**

Office 2013

Office 2016

Office 2019

Office 2021

Office 2024

## **3. 如何使用该激活方式：**

[图文激活过程](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fwww.bktai.com%2FPost%2F52) 在需要激活时打开管理员模式的**PowerShell**并执行如下命令：

```powershell
irm https://get.activated.win | iex
```

PowerShell

在命令提示符窗口中输入 3 然后按照提示进行操作即可，正常情况下脚本会自动检测系统或软件版本执行操作，后续基本不需要人工干预。

## **4. 激活原理**

MAS 团队对微软激活保护系统进行深入研究发现了微软用于激活产品和存储许可证的具体技术细节([https://massgrave.dev/blog/tsforge](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fmassgrave.dev%2Fblog%2Ftsforge))，然后还在微软的保护系统里发现漏洞并可以进行利用。

微软的现代 DRM 技术被称为软件保护平台 SPP，这个复杂的系统由多个组件组成，产品激活信息则存储在物理存储 data.dat 和令牌存储 tokens.dat **(以前我们备份激活信息时操作的就是这两个文件)**。

TSForge 技术可以将伪造的数据注入到这些存储文件中，这可以绕过所有检查并迫使 SPP 平台将假产品密钥或电话确认 ID 识别为有效许可证。

有趣的是 MAS 团队此前还预告了也成功破解 Windows 10 ESU 付费扩展安全更新，在新的博客文章中 MAS 透露其实这也是利用 TSForge 实现的。

未来对用户来说想要激活系统是个非常简单的事情，当然说到底这是因为微软不在乎个人用户是否使用 **盗版**，正如微软员工所说，只要你使用 Windows 11 就够了，因为你就是产品。

MAS 项目的工具都是开源的并且托管在 GitHub 平台，事实上如果微软想要打击这种技术盗版那直接给 GitHub 发送 DMCA 通知就行了，不过微软从来没这么做过。
