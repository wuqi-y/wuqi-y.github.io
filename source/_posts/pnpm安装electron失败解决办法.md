---
abbrlink: ''
categories:
- - 前端
cover: https://s11.ax1x.com/2023/12/28/piqdFC8.jpg
date: '2023-12-25T15:39:42.693989+08:00'
recommend: ''
swiper: ''
tags:
- electron
title: pnpm（npm）安装electron失败解决办法
updated: 2023-12-28T9:10:31.98+8:0
---
### pnpm（npm）安装 electron 失败解决办法

安装`electron`老是报网络错误，提供一个方法亲测可用

`pnpm config set electron_mirror "https://npm.taobao.org/mirrors/electron/"`

`npm config set electron_mirror "https://npm.taobao.org/mirrors/electron/"`

然后

`pnpm i electron -D`

或

`npm i electron -D`

执行的时候在脚本中添加自定义命令 `electron .`即可
