---
abbrlink: ''
categories:
- - 前端
cover: https://api.qjqq.cn/api/Img?t=8989
date: '2024-01-02T17:54:43.258898+08:00'
recommend: ''
swiper: ''
tags:
- node
- PM2
title: PM2常用命令
updated: 2024-1-2T18:5:25.4+8:0
---
### PM2常用命令

1. 启动应用程序：

` pm2 start app.js`

这将启动名为 `app`的应用程序，并将其作为一个后台进程运行。

2. 列出所有应用程序：

   `pm2 list`

这将列出所有正在运行的应用程序，包括它们的ID、名称、状态和启动时间等信息。

3. 停止应用程序：

   `pm2 stop app`

这将停止名为 `app`的应用程序。

4. 重启应用程序：

   `pm2 restart app`

这将重启名为 `app`的应用程序。

5. 删除应用程序：

   `pm2 delete app`

这将停止并删除名为 `app`的应用程序。

6. 监视应用程序日志：

   `pm2 logs app`

这将显示名为 `app`的应用程序的日志输出。

7. 监视所有应用程序日志：

   `pm2 logs`

这将显示所有正在运行的应用程序的日志输出。

8. 监视应用程序的CPU和内存使用情况：

   `pm2 monit app`

这将显示名为 `app`的应用程序的CPU和内存使用情况。

9. 使用PM2启动应用程序，并将日志输出到文件夹中

   `pm2 start app.js --name myapp --log logs/myapp.log`

这将启动名为`myapp`的应用程序，并将日志输出到`logs/myapp.log`文件中。请确保将`app.js`替换为你的应用程序的入口文件
