---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:54:24.711752+08:00'
tags:
- Typora
title: 如何在Typora中添加自定义搜索引擎
updated: '2025-08-27T19:54:25.039+08:00'
---
[![](https://www.alicetec.cn/upload/Group-screen_%E7%BB%93%E6%9E%9C.webp)](https://www.alicetec.cn/upload/Group-screen_%E7%BB%93%E6%9E%9C.webp)

具体可见：官方教程

[![](https://support.typoraio.cn/assets/img/favicon-16.png)Add Search Service - Typora SupportUsers can add custom search engines to extend functions shown in context menu. macOS There is a system-wide preference to change available search engines in the context menu for most applications: Windows / Linux Open Menu → Preference in Typora, then click “Open Advanced Settings”. Open and edit conf.user.json from the “File Explorer”. If there’s no such file, create one. Modify or set following config into the conf.user.json file, %s will represent the selected text. for example:](https://support.typoraio.cn/Add-Search-Service/)笔者发了邮件咨询，官方很快回复，给一个赞👍b(￣▽￣)d

以下内容在官方教程的基础上给予翻译与少量修改

# 用户可以添加自定义搜索引擎，以扩展上下文菜单中显示的功能。

**Users can add custom search engines to extend functions shown in context menu.**

[![Slice 2](https://support.typoraio.cn/media/add-search-service/Slice%202.png)](https://support.typoraio.cn/media/add-search-service/Slice%202.png)

# macOS（苹果桌面操作系统）

There is a system-wide preference to change available search engines in the context menu for most applications:

在大多数应用程序的右键菜单中，都有一个全局首选项来更改可用的搜索引擎：

[![Snip20160815_11](https://support.typoraio.cn/media/add-search-service/Snip20160815_11.png)](https://support.typoraio.cn/media/add-search-service/Snip20160815_11.png)

# Windows / Linux

1. Open `Menu` → `Preference` in Typora, then click “Open Advanced Settings”. 在 Typora 中打开`菜单` → `偏好设置`，然后单击 “打开高级设置”。
   [![sshot-1](https://support.typoraio.cn/media/custom-key-binding/sshot-1.png)](https://support.typoraio.cn/media/custom-key-binding/sshot-1.png)
2. Open and edit `conf.user.json` from the “File Explorer”. If there’s no such file, create one. 从 “文件资源管理器 ”中打开并编辑 `conf.user.json`。如果没有此类文件，请创建一个。[![](https://www.alicetec.cn/upload/explorer_xK27YyUade.png)](https://www.alicetec.cn/upload/explorer_xK27YyUade.png)
3. Modify or set following config into the `conf.user.json` file, `%s` will represent the selected text. for example: 在 `conf.user.json` 文件中修改或设置以下配置，`%s` 代表所选文本（即你要检索的东西将会填入到此）：

   ```perl
   "searchService": [
       ["Search with Google", "https://google.com/search?q=%s"],
       ["Translate", "http://translate.google.com/?source=osdd#auto|auto|%s"]
       ["Search with Wikipedia", "https://en.wikipedia.org/wiki/Special:Search/%s"]
     ]
   ```
   Note: Default config is: 注：默认配置为

   ```perl
   "searchService": [
       ["Search with Google", "https://google.com/search?q=%s"],
     ]
   ```
4. Restart Typora, and then the options from `searchService` will be available from the context menu. 重新启动 Typora，然后就可以从右键菜单中使用 `searchService` 的选项了。
