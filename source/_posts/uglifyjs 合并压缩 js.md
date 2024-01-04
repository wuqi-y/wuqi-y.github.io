---
abbrlink: ''
categories:
- - 前端
cover: https://s11.ax1x.com/2023/12/27/pibLfsg.jpg
date: '2023-12-18T15:17:44.903023+08:00'
recommend: ''
swiper: ''
tags:
- js
title: uglifyjs 合并压缩 js
updated: 2023-12-27T18:5:14.237+8:0
---
### 1、全局安装 uglify-js

`npm install -g uglify-js`

###### 也可以局部安装

`npm install --save-dev uglify-js`

### 2、在终端执行合并压缩命令

`uglifyjs js/common.js js/example.js -o js/common.min.js`

上面的命令表示把 common.js 和 example.js 合并成为 common.min.js。

这里面的路径请根据你项目的实际情况更改

#### 一些常用的参数列表

```cmd
-o,--output      指定输出文件，默认情况下为命令行
-b,--beautify    美化代码格式的参数
-m,--mangle      改变变量名称（ex：在一些例如YUI Compressor压缩完的代码后你可以看到
a,b,c,d,e,f之类的变量，加了-m参数，uglifyjs也可以做到，默认情况下，是不会改变变量名称的）
-r,--reserved    保留的变量名称，不需要被-m参数改变变量名的
-c,--compress    OK，主角登场了，这是让uglifyjs进行代码压缩的参数。可以在-c后边添加
一些具体的参数来控制压缩的特性，下文中会具体介绍。
--comments       用来控制注释的代码的
```

参考链接 [UglifyJS]([https://](https://github.com/mishoo/UglifyJS))
