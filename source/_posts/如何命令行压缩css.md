---
abbrlink: 压缩css
categories:
- - 前端
cover: https://s11.ax1x.com/2023/12/27/pibqrCV.jpg
date: '2023-12-13T17:16:10.190907+08:00'
recommend: ''
swiper: ''
tags:
- css
title: clean-css 合并压缩css
updated: 2023-12-27T18:9:6.431+8:0
---
### 1、全局安装 clean-css

`npm install -g clean-css`

###### 也可以局部安装

`npm install --save-dev clean-css`

#### 2、安装 clean-css-cli

`npm install -g clean-css-cli`

### 3、在终端执行合并压缩命令

`cleancss -o css/app.all.min.css css/common.css css/index.css`

css/app.all.min.css --- 表示你压缩后的目标路径及 css 文件名

css/common.css css/index.css --- 这些都是你需要压缩合并的 css
