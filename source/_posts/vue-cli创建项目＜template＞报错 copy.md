---
categories:
- 前端
comment: true
author: Yang · Mr
cover: true
img: /medias/banner/9.jpg
date: '2023-10-8 11:33:00'
recommend: true
tags:
- 前端
title: vue/cli创建项目＜template＞报错
---
##### 启动项目就报这种错误


![err](/medias/csd/1.png)

![err](/medias/csd/2.png)

###### 一、首先在vuter插件中 扩展设置中吧template勾选去掉(默认是勾选的)


如下（示例）

![err](/medias/csd/3.png)

然后重启vscode 如果还是不行的话 下一步
 
 ```json
 "vueCompilerOptions": {
  "experimentalDisableTemplateSupport": true
  }
 ```
然后重启vscode 就好了