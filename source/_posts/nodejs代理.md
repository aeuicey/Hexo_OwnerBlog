---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:37:59.713312+08:00'
tags:
- 代理
- Nodejs
title: 【Node.js】：配置源（registry）、代理（proxy）
updated: '2025-08-27T19:38:00.220+08:00'
---
## --

created: 2025-07-08T09:27:40 (UTC +08:00)
tags: [npm,https,yarn,网络安全]
source: [https://cloud.tencent.com/developer/article/1781066](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fcloud.tencent.com%2Fdeveloper%2Farticle%2F1781066)

# 【Node.js】：配置源（registry）、代理（proxy）

> ## Excerpt
>
> 换npm、yarn的镜像源，或配置npm、yarn的代理，都是为了解决 npm 依赖下载慢的问题。


**1. 背景**

换npm、yarn的镜像源，或配置npm、yarn的代理，都是为了解决 npm 依赖下载慢的问题。

* 如果你要下载的依赖，都能在“淘宝”或者“cnpm”镜像源上找到，那么***换镜像源***就能加速很多。
* 如果你必须通过“npm镜像源”下载依赖（例如：你依赖的某特定版本的库，淘宝、cnpm镜像源上还没来得及与 npm 镜像源同步），那么你就需要***配置代理***，***科学上网***（如果你有[VPN](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Fvpn%3Ffrom_column%3D20065%26amp%3Bfrom%3D20065)，那更省事）。

**2. npm**

**2.1. 配置镜像源**

* **方式1：npm 命令**

```javascript
// 查看镜像源 npm config get registry // 设置镜像源 npm config set registry http://registry.npm.taobao.org/ npm config set registry https://registry.npmjs.org/
```

* **方式2：nrm 工具**
  * nrm can help you easy and fast switch between different npm registries, now include: npm, cnpm, taobao, nj(nodejitsu).

```javascript
npm install -g nrm // 安装 nrm ls // 查看已有的源 nrm use <registry> // 切换源 nrm add <registry> <url> // 添加源 nrm del <registry> // 删除源 nrm test [registry] // 测速
```

**2.2. 配置代理**

```javascript
// 查看代理 npm config get proxy npm config get https-proxy // 设置代理 npm config set proxy http://127.0.0.1:8080 npm config set https-proxy http://127.0.0.1:8080 // 删除代理 npm config delete proxy npm config delete https-proxy
```

**3. yarn**

**3.1. 配置镜像源**

```javascript
// 查看镜像源 yarn config get registry // 设置镜像源 yarn config set registry http://registry.npm.taobao.org/ yarn config set registry https://registry.npmjs.org/
```

**3.2. 配置代理**

```javascript
// 查看代理 yarn config get proxy yarn config get https-proxy // 设置代理 yarn config set proxy http://127.0.0.1:8080 yarn config set https-proxy http://127.0.0.1:8080 // 删除代理 yarn config delete proxy yarn config delete https-proxy
```

**参考：**

> NPM registry manager（nrm）： [https://github.com/Pana/nrm](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fgithub.com%2FPana%2Fnrm) npm Docs： [https://docs.npmjs.com/cli/v6/using-npm/config#proxy](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fdocs.npmjs.com%2Fcli%2Fv6%2Fusing-npm%2Fconfig%23proxy) [https://docs.npmjs.com/cli/v6/using-npm/config#https-proxy](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fdocs.npmjs.com%2Fcli%2Fv6%2Fusing-npm%2Fconfig%23https-proxy)

本文参与 [腾讯云自媒体同步曝光计划](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fcloud.tencent.com%2Fdeveloper%2Fsupport-plan)，分享自微信公众号。

原始发表：2021-01-18，如有侵权请联系 [cloudcommunity@tencent.com](mailto:cloudcommunity@tencent.com) 删除
