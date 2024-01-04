---
abbrlink: ""
categories: []
cover: https://s11.ax1x.com/2023/12/27/pibqygU.jpg
date: "2023-11-02T10:01:59.143312+08:00"
tags:
  - npm
title: 如何查看npm的镜像信息
updated: 2023-11-2T10:4:11.149+8:0
---

要查看 npm 的镜像信息，你可以使用`npm config get registry`命令。这个命令会返回当前配置的 npm 镜像地址。

如果你想要切换 npm 的镜像源，有以下几种选择：

- `npm config set registry <registry-url>`：将 npm 的镜像源设置为指定的`<registry-url>`。
- `npm config delete registry`：删除已设置的 npm 镜像源，恢复默认的官方源。

常见的 npm 镜像源包括：

- 官方源（[https://registry.npmjs.org/）](https://registry.npmjs.org/%EF%BC%89)
- 淘宝 NPM 镜像源（[https://registry.npm.taobao.org/）](https://registry.npm.taobao.org/%EF%BC%89)
- cnpmjs 镜像源（[https://r.cnpmjs.org/）](https://r.cnpmjs.org/%EF%BC%89)

使用合适的 npm 镜像源可以加快依赖包的下载速度，提高开发效率。
