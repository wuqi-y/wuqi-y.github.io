---
abbrlink: ""
categories:
  - - 前端
cover: https://api.qjqq.cn/api/Img?p=3
date: "2023-12-26T09:16:12.255934+08:00"
recommend: "88"
swiper: "66"
tags:
  - electron
title: 如何使用electron将web打包成exe桌面程序
updated: 2023-12-26T9:16:5.899+8:0
---

### 如何使用 electron 将 web 打包成 exe 桌面程序

首先安装依赖 使用 `npm`或者 `yarn`安装

`npm i electron@28.1.0 -D`

`npm i electron-packager@17.1.2 -D`

例如 `index.html`文件如下

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello Worl00d!</h1>
    We are usin000g io.js .
  </body>
</html>
```

在主文件夹创建一个 `index.js`文件

```js
const { app } = require("electron");
var BrowserWindow = require("electron").BrowserWindow; // 创建原生浏览器窗口的模块

// 保持一个对于 window 对象的全局引用，不然，当 JavaScript 被 GC，
// window 会被自动地关闭
var mainWindow = null;

// 当所有窗口被关闭了，退出。
app.on("window-all-closed", function () {
  // 在 OS X 上，通常用户在明确地按下 Cmd + Q 之前
  // 应用会保持活动状态
  if (process.platform != "darwin") {
    app.quit();
  }
});

// 当 Electron 完成了初始化并且准备创建浏览器窗口的时候
// 这个方法就被调用
app.on("ready", function () {
  // 创建浏览器窗口。
  mainWindow = new BrowserWindow({ width: 800, height: 600 });

  // 加载应用的 index.html
  mainWindow.loadURL("file://" + __dirname + "/index.html");

  // 打开开发工具
  mainWindow.openDevTools();

  // 当 window 被关闭，这个事件会被触发
  mainWindow.on("closed", function () {
    // 取消引用 window 对象，如果你的应用支持多窗口的话，
    // 通常会把多个 window 对象存放在一个数组里面，
    // 但这次不是。
    mainWindow = null;
  });
});
```

然后把下面脚本命令替换到你的 `package.json`里面

`npm run serve` 运行调试

```json
"scripts": {
    "serve": "electron .",
    "build": "electron-packager ./ app --platform=win32 --arch=x64 --out=dist/"
  },
```

`npm run build` 进行打包

electron-packager ./ app --platform=win32 --arch=x64 --out=dist/

`./`是需要执行的 electron 代码文件的目录 这里直接同级即可

`app`是打包后 exe 程序的名字

`--platform=win32 --arch=x64`是打包的系统详情请 [查看官网](https://www.npmjs.com/package/electron-packager)

`--out=dist` dist 是打包后的文件夹名称

> 注意 这里仅是最基础的演示阶段 如果需要更完整的生态以及开发流程 请查看官网 [官网](https://www.electronjs.org/zh/docs/latest/)

**如果想要查看如何打包为一个 exe 可执行文件 请看我上篇文章[# electron 打包为 exe 可执行文件](/2023/12/25/electron-da-bao-wei-exe-ke-zhi-xing-wen-jian/)**
