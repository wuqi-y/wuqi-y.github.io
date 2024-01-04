---
abbrlink: ""
aplayer: null
aside: null
categories:
  - 学习笔记
comments: null
cover: https://s11.ax1x.com/2023/12/27/pib7hUP.jpg
date: 2023/10/17
description: null
highlight_shrink: null
katex: null
keywords: null
mathjax: null
random: null
recommend: "100"
swiper: "70"
tags:
  - Vue
test:
  t: "1"
  t2: "12"
title: vue/cli创建项目＜template＞报错
type: null
updated: 2023-12-22T11:54:10.515+8:0
---

##### 启动项目就报这种错误

![err](/img/csd/1.png)

![err](/img/csd/2.png)

###### 一、首先在 vuter 插件中 扩展设置中吧 template 勾选去掉(默认是勾选的)

如下（示例）

![err](/img/csd/3.png)

然后重启 vscode 如果还是不行的话 下一步

```json
"vueCompilerOptions": {
 "experimentalDisableTemplateSupport": true
 }
```

然后重启 vscode 就好了
