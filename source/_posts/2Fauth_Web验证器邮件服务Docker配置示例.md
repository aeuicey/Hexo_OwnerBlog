---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:52:07.757600+08:00'
tags:
- 邮件服务
- 2Fauth
- Docker
title: 2Fauth_Web验证器邮件服务Docker配置示例
updated: '2025-08-27T19:52:08.303+08:00'
---
[![](https://www.alicetec.cn/upload/image-Xjbl.png)](https://www.alicetec.cn/upload/image-Xjbl.png)

# 参考配置

[![](https://bbs.fit2cloud.com/uploads/default/optimized/1X/45a64ba9dc447d9aa003da87bfab0f8a75064f02_2_32x32.png)市场里装的2FAuth收不到系统邮件，请问我这么配置正常吗？ - 1Panel - 社区论坛 - FIT2CLOUD 飞致云environment: - MAIL\_MAILER=SMTP - MAIL\_HOST=smtp.qiye.aliyun.com - MAIL\_PORT=465 - MAIL\_USERNAME=services@xxx.xxx - MAIL\_PASSWORD=password123 - MAIL\_ENCRYPTION=SSL - MAIL\_FROM\_NAME=2FAuth - MAIL\_FROM\_ADDRESS=services@xxx.xxx](https://bbs.fit2cloud.com/t/topic/7186)

```graphql
environment: - MAIL_MAILER=smtp - MAIL_HOST=smtp.qiye.aliyun.com - MAIL_PORT=465 - MAIL_USERNAME=services@xxx.xxx - MAIL_PASSWORD=password123 - MAIL_ENCRYPTION=ssl - MAIL_FROM_NAME=2FAuth - MAIL_FROM_ADDRESS=services@xxx.xxx
```


# 作者配置

笔者使用1panel\_Docker快速部署，默认配置方案没有邮件服务。需要自行在容器变量处配置。

## QQ邮箱SMTP配置变量参考：

```ini
DB_DATABASE="/srv/database/database.sqlite"
APP_NAME=AliceAuth
APP_URL=https://auth.alicetec.cn ##填入你的外部访问地址
IS_DEMO_APP=false
AUTHENTICATION_GUARD=web-guard
LOG_CHANNEL=daily
APP_KEY=************************ ##此处为加密键值需要妥善保存
SESSION_DRIVER=file
CACHE_DRIVER=file
LOG_LEVEL=notice
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
APP_ENV=local
APP_TIMEZONE=UTC
APP_DEBUG=false
SITE_OWNER=Alice***@outlook.com 
DB_CONNECTION=sqlite

##以下为邮件配置
MAIL_MAILER=smtp   ##键入协议
MAIL_HOST=smtp.qq.com  ##键入服务提供商主机
MAIL_PORT=465      ##键入提供商端口
MAIL_USERNAME=2558*******  ##键入用户名
MAIL_PASSWORD=rpga********   ##键入密码，部分需要申请相关密钥
MAIL_ENCRYPTION=ssl  ##键入加密方式 
MAIL_FROM_NAME=2558******@qq.com  ##随便
MAIL_FROM_ADDRESS=2558*******@qq.com  ##随便
MAIL_VERIFY_SSL_PEER=true ##默认即可
##下面保持默认即可
THROTTLE_API=60
LOGIN_THROTTLE=5
AUTHENTICATION_LOG_RETENTION=365
AUTH_PROXY_HEADER_FOR_USER=null
AUTH_PROXY_HEADER_FOR_EMAIL=null
PROXY_LOGOUT_URL=null
WEBAUTHN_NAME=2FAuth
WEBAUTHN_ID=null
WEBAUTHN_USER_VERIFICATION=preferred
TRUSTED_PROXIES=null
PROXY_FOR_OUTGOING_REQUESTS=null
CONTENT_SECURITY_POLICY=true
BROADCAST_DRIVER=log
QUEUE_DRIVER=sync
SESSION_LIFETIME=120
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1
VITE_PUSHER_APP_KEY=
VITE_PUSHER_APP_CLUSTER=
MIX_ENV=local
VERSION=5.5.2
CREATED=2025-04-11T22:00:23Z
COMMIT=b014497
```
