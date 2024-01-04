---
abbrlink: ""
categories:
  - - 前端
  - - 学习笔记
comment: true
cover: https://s11.ax1x.com/2023/12/27/pib72DA.jpg
date: "2023-08-01 11:33:00"
recommend: true
tags:
  - 运维
  - 前端
title: Jenkins如何自动化部署前端项目(安装Jenkins)
top: true
updated: 2023-10-24T17:57:33.719+8:0
---

### Jenkins 如何自动化部署前端项目

#### 1、安装 JDK 11 这里我们通过 yum 系统 Centos 8.4.64

1. 首先，确保你的系统已经更新到最新的软件包列表。可以运行以下命令来更新软件包列表：

```cmd
sudo yum update
```

###### 安装 JDK 11

```cmd
sudo yum install java-11-openjdk-devel
```

2. 安装过程中，系统会提示你确认是否继续安装。输入`Y`并按下 Enter 键，然后等待安装完成。
3. 安装完成后，可以使用以下命令来验证 JDK 11 的安装：

###### 验证 Java 是否安装成功

```cmd
java -version
```

输出应该显示类似以下内容：

```cmd
openjdk version "11.x.x" 2021-XX-XX
OpenJDK Runtime Environment (build 11.x.x+XX-XXXX)
OpenJDK 64-Bit Server VM (build 11.x.x+XX-XXXX, mixed mode, sharing)
```

###### 卸载 Jdk

```cmd
# 查看CentOS自带JDK是否已安装:
yum list installed | grep java
# 如果存在自带的jdk，删除自带的jdk
yum -y remove java-1.8.0-openjdk*
yum -y remove tzdata-java.noarch
```

#### 2、安装 Jenkins

首先，添加 Jenkins 的官方软件包源。打开终端窗口，并使用以下命令导入 Jenkins 的 GPG 密钥：

```cmd
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io-2023.key
```

然后安装 安装过程中，系统会提示你确认是否继续安装。输入`Y`并按下 Enter 键，然后等待安装完成

`sudo yum install jenkins`

###### 启动命令

您可以使用以下命令启动 Jenkins 服务：

```cmd
sudo systemctl start jenkins
```

###### 您可以使用以下命令检查 Jenkins 服务的状态：

`sudo systemctl status jenkins`

如下：

![图](/img/demo.png)
