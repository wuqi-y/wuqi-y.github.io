---
abbrlink: ""
categories:
  - - 学习笔记
cover: https://s11.ax1x.com/2023/12/27/pib7fEt.jpg
date: "2023-11-02T09:45:26.993702+08:00"
tags:
  - windowns
title: Windows操作系统生成SSH密钥
updated: 2023-11-2T9:52:34.487+8:0
---

**在 Windows 上生成 SSH 密钥可以通过以下简单步骤：**

1. 创建公钥（如果在 cmd 窗口不可执行，请下载 gitbash 执行）

```cmd
ssh-keygen -t rsa -C "youremail@example.com"
```

2. 输入完毕后按回车，到底即可，此时 c 盘——用户——用户名——.ssh 文件夹 里面生成好了“id*rsa”和“id_rsa.pub”文件（*不一定是一样的位置，会有提示请以自己的目录为准\_）。
3. 将公钥添加到需要访问的服务器上的 authorized_keys 文件中。
4. 使用私钥进行 SSH 连接。
