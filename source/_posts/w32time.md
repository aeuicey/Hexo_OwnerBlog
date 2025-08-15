---
abbrlink: ''
categories:
- - 技术
date: '2025-08-16T06:50:46.838564+08:00'
tags:
- 技术
- windows
- 微软
- 时间同步
title: W32Time：同步：工作组计算机上可能会忽略 SpecialPollInterval
updated: '2025-08-16T06:50:47.305+08:00'
---
[![](https://gcore.jsdelivr.net/gh/aeuicey/Picwent/pic/20250815173649939.png)](https://gcore.jsdelivr.net/gh/aeuicey/Picwent/pic/20250815173649939.png)

本文可帮助修复 NTP 客户端未按预期同步 SpecialPollInterval 期间的时间的问题。

*原始 KB 数：* 3205089

## **现象**

假设修改 W32time 设置以始终运行，并且以下条件之一为 true：

* 使用默认工作站设置。
* 使用具有大型 SpecialPollInterval 设置值的自定义 NTP 同步设置。

在此方案中，NTP 客户端不会按预期同步 SpecialPollInterval 期间的时间。

## **原因**

由于 Windows 时间服务处理大型 SpecialPollInterval 值的方式，时间可能会以比预期更长的间隔从 NTP 服务器同步。

## **解决方法**

### **解决方法 1**

指定比默认值更小的 SpecialPollInterval 值。 默认值如下：

MinPollInterval = 0xA （== 2^10 秒 == 1024 秒）
MaxPollInterval = 0xF （== 2^15 秒 == 32768 秒）
SpecialPollInterval = 604800 秒

指定一个 SpecialPollInterval 值，该值位于 MinPollInterval 和 MaxPollInterval 之间。 示例值为 3600 秒（== 1 小时）。

若要使用新设置配置 W32time，请执行以下步骤：

1. 启动“注册表编辑器”。
2. 更改以下注册表项的值：
   `HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient`
   值名称：SpecialPollInterval
   默认值：604800
   修改值：3600
3. 重启 Windows 时间服务，或运行以下命令来向 W32time 发出有关修改后的配置的信息：

   ```bash
   w32tm /config /update  
   ```

   Bash

### **解决方法 2**

使用基于 MinPollInterval、MaxPollInterval 而不是使用 SpecialPollInterval 的内置轮询间隔调整。 如果客户端计算机保持相当准确的时间，此内置工具会自动调整从 MinPollInterval 到 MaxPollInterval 的轮询间隔。 只需修改 NtpServer 配置中的标志才能从 SpecialPollInterval 切换到自动轮询间隔，如下所示：

1. 启动“注册表编辑器”。
2. 更改以下注册表项的值：
   `HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W32Time\Parameters`
   值名称：NtpServer
   默认值： `time.windows.com`、0x9
   修改的值： `time.windows.com`、0x8
3. 重启 Windows 时间服务，或运行以下命令：
   ```bash
   w32tm /config /update  
   ```
