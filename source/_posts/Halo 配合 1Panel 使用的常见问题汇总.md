---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:59:53.307859+08:00'
tags:
- Halo
- 1panel
title: Halo 配合 1Panel 使用的常见问题汇总
updated: '2025-08-27T19:59:53.827+08:00'
---
---
created: 2025-01-21T02:15:36 (UTC +08:00)

tags: [建站,网站,主题,博客主题,博客模板,网站主题,网站模板,免费建站,开源建站,开源]

source: https://www.halo.run/archives/halo-1panel-faq

author: **Ryan Wang**
---
[**1Panel**](https://www.alicetec.cn/linkJump?target=https%3A%2F%2F1panel.cn%2F) 是一个现代化、开源的 Linux 服务器运维管理面板，使用它可以非常方便地部署和更新 Halo，但在使用过程中仍然有一些注意事项需要了解，这篇文章将介绍 Halo 配合 1Panel 的使用中，一些可能出现的问题，以及对应的解决方案。

## **正确设置外部访问地址**

Halo 中的外部访问地址用于在系统内部确定一个实际的访问地址，在通知邮件、主题中都可能用到，所以在 1Panel 创建 Halo 应用的时候不要忽略外部访问地址选项，你应该设置为访问网站的实际地址，比如 `https://demo.halo.run`。

[![](https://www.halo.run/upload/1panel-create-halo-external-url.png)](https://www.halo.run/upload/1panel-create-halo-external-url.png)

如果你在创建 Halo 应用的时候遗漏了这个配置，也可以在应用的参数配置中修改并重建 Halo 应用。

[![](https://www.halo.run/upload/1panel-update-halo-external-url.png)](https://www.halo.run/upload/1panel-update-halo-external-url.png)

## **WAF 防火墙配置**

WAF 即 Web 应用防火墙，可以保护你的网站免受恶意攻击，如 SQL 注入、XSS 攻击等，但在 Halo 控制台有不少接口需要传输 HTML 内容，这很容易导致误判，如果你遇到下面这些问题，代表被 1Panel 的 WAF 功能拦截，**导致流量并没有经过 Halo**，建议在 1Panel 的 WAF 功能的拦截记录中查看问题详情，并自行决定处理措施。

### **保存文章失败**

[![](https://www.halo.run/upload/1panel-waf-1.png)](https://www.halo.run/upload/1panel-waf-1.png)

[![](https://www.halo.run/upload/1panel-waf-2.png)](https://www.halo.run/upload/1panel-waf-2.png)

原因为 Halo 的文章内容为 HTML 格式，被 WAF 的 XSS 注入规则拦截。

**处理建议：在 WAF -> 网站设置 -> 默认规则中，自行了解和判断是否要启用这些规则，或者在自定义规则中为这些接口添加策略。**

## **关闭网站防篡改**

1Panel 的网站防篡改功能是为了保护网站目录，不允许任何外部程序对受保护的目录进行修改，因为 Halo 在整个运行过程中，可能涉及到附件上传/删除，主题安装/卸载、备份恢复等功能，这些功能都会去操作应用目录，所以不要为 Halo 的应用目录开启网站防篡改功能。

[![](https://www.halo.run/upload/1panel-dir-protection-1.png)](https://www.halo.run/upload/1panel-dir-protection-1.png)

以下是开启防篡改之后，Halo 可能出现的异常表现：

[![](https://www.halo.run/upload/1panel-dir-protection-3.png)](https://www.halo.run/upload/1panel-dir-protection-3.png)

开启防篡改之后，主题无法删除

[![](https://www.halo.run/upload/1panel-dir-protection-2.png)](https://www.halo.run/upload/1panel-dir-protection-2.png)

开启防篡改之后，附件无法删除

**处理建议：不要为 Halo 应用目录开启防篡改功能。**

## **文件上传大小限制**

1Panel 的 Web 服务器 OpenResty 默认设置了 `client_max_body_size` 参数，如果你在 Halo 中上传文件出现了下面的提示，则代表被 OpenResty 拦截。

[![](https://www.halo.run/upload/1panel-client-max-body-size.png)](https://www.halo.run/upload/1panel-client-max-body-size.png)

[![](https://www.halo.run/upload/1panel-client-max-body-size-2.png)](https://www.halo.run/upload/1panel-client-max-body-size-2.png)

**处理建议：在 1Panel 的网站设置中，调整** `client_max_body_size` **参数，具体大小可以根据自己的情况调整。**
