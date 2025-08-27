---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:50:32.899062+08:00'
tags:
- 美化
- Steam
title: 美化：修改steam客户端样式
updated: '2025-08-27T19:50:33.355+08:00'
---
鉴于某次Steam更新，导致原有的“皮肤”功能被踢除。为了不再忍受Steam现在客户端“过时”的审美，笔者不得不寻找新的Steam Hook方案。直到我找到了它——**Millennium** **An open source gateway to a better Steam® client experience.**

[![](https://www.alicetec.cn/upload/image-ZVaq.png)](https://www.alicetec.cn/upload/image-ZVaq.png)

# 什么是Millennium？

Millennium 于 2023 年 4 月正式推出，是一个开源的低代码 Mod 框架，用于创建、管理和使用桌面 Steam 客户端的主题/插件，无需任何内部交互或开销。

Millennium 基于 Steam 客户端内部允许其运行的漏洞。

正如[此处](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fchromedevtools.github.io%2Fdevtools-protocol%2F)的非官方记录，我们可以以编程方式与 Steam 客户端交互，而无需修改其内部存储器。这允许我们创建一个 SDK，用于将 CSS 和 JS 注入上下文窗口。

简单的说，这是一个DLL管理器，可以帮助你安装你所需要的Steam皮肤与插件，最终达到美化与提升功能性的效果。

话不多说，上使用效果图：

[![](https://www.alicetec.cn/upload/TM5aK3Q3ON_%E7%BB%93%E6%9E%9C.webp)](https://www.alicetec.cn/upload/TM5aK3Q3ON_%E7%BB%93%E6%9E%9C.webp)[![](https://www.alicetec.cn/upload/msedge_gGto4zkOxh_%E7%BB%93%E6%9E%9C.webp)](https://www.alicetec.cn/upload/msedge_gGto4zkOxh_%E7%BB%93%E6%9E%9C.webp)

# 如何安装

要在 Windows 上安装 Millennium，可以使用官方 PowerShell 安装程序脚本。要运行该脚本，请打开 PowerShell，粘贴以下命令，然后按 Enter。

此安装程序是完全开源的，官方鼓励社区审核[![](https://github.githubassets.com/favicons/favicon.png)Millennium/scripts/install.ps1 at main · SteamClientHomebrew/Millennium · GitHub](https://github.com/SteamClientHomebrew/Millennium/blob/main/scripts/install.ps1)。目前代码托管在Github上。

### 自动安装

**Millennium 是完全可移植的，以下脚本不会更改任何系统配置。**

**请在Powershell下运行以下代码：**

```bash
iwr -useb "https://steambrew.app/install.ps1" | iex
```

### **手动安装**

首先，从[此存储库](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fgithub.com%2FSteamClientHomebrew%2FMillennium%2Freleases%2Flatest)下载 Millennium 的 Windows 压缩包。只需将所有文件放入您的 Steam 目录中，然后重启Steam，接下来你应该就可以看到弹出的提示了。

# 开始使用

## **主题**

要为您的 Steam 客户端选择要使用的主题，请从设置**中主题选项卡**的下拉列表中选择一个主题。

如果您还没有任何主题，则需要安装一些主题。前往 [https://steambrew.app/themes](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fsteambrew.app%2Fthemes) 并选择一些您喜欢的主题。

**安装主题**

1. 在安装了 Millennium 的情况下打开 Steam 并导航到 [https://steambrew.app/themes](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fsteambrew.app%2Fthemes)
2. 选择您要使用的主题，单击 **Install** 安装，然后等待该过程完成。（请保证网络环境良好。如果自动安装失败，可以前往皮肤Github仓库下载源文件并将其复制到 Millennium 的Skin文件夹中）
3. 前往 Steam 设置 -> 主题 -> 客户端主题 并选择您新安装的主题。

**信息**

如果您使用的是 带有广告拦截器的浏览器（这会阻止一些动作的运行），则可能难以安装开箱即用的主题，特别是网站说您在 Steam 打开时处于预览模式。要解决这个问题，请打开广告拦截器，然后“允许所有跟踪器和广告”

您也可以禁用站点的整个保护。经笔者测试，网站本身没有什么广告，因此关开不影响。

---

## **插件**

1. 打开 安装了 Millennium 的 Steam 并导航到 [https://steambrew.app/plugins](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fsteambrew.app%2Fplugins)。[![msedge_YxWIRl0DWi_结果.webp](https://www.alicetec.cn/upload/msedge_YxWIRl0DWi_%E7%BB%93%E6%9E%9C.webp)](https://www.alicetec.cn/upload/msedge_YxWIRl0DWi_%E7%BB%93%E6%9E%9C.webp)
2. 选择您要使用的插件，单击 **Download**。
3. 提示选择下载位置后，导航到您的 Steam 插件文件夹，该文件夹应如下所示：`“C：\Program Files （x86）\Steam\plugins”`
4. 将文件安装到 plugins 文件夹中后，必须将 zip 文件解压缩到以安装的插件命名的新文件夹中。
5. 前往 Steam 设置 -> 插件并启用新安装的插件。注意：您可能需要完全重新启动 Steam 才能使插件生效。

## **更新**

内置自动更新提醒选项，当然如果不堪其扰可以选择关闭。为了避免因为Steam更新导致的主题与插件异常，尽量使用最新版本。
