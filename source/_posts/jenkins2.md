---
abbrlink: ""
categories:
  - - 运维
  - - 学习笔记
comment: true
cover: https://s11.ax1x.com/2023/12/27/pib7RHI.jpg
date: "2023-08-01 11:33:00"
recommend: true
tags:
  - 运维
  - 前端
title: Jenkins如何自动化部署前端项目(2)
updated: 2023-10-24T17:56:29.223+8:0
---

### Jenkins 如何自动化部署前端项目

前置步骤我们都操作完了，这篇开始介绍 jenkins 的是哟。话不多说，看操作(没安装的请看我主页有详细的安装教程)

1、登录进入 jenkins 后会让你选择安装插件，选择第一个默认的就行。

2、配置 JDK 和 Git 都需要执行路径，所以需要先把执行路径找到，先进入服务器的终端界面执行

> JDK 的路径

```
 echo $JAVA_HOME
```

如果是空记得先去设置 java 的环境变量 `which java` 查看 java 的安装路径

![jdk路径](/img/j/1.png)

> Git 的路径

```
 which git
```

![git路径](/img/j/2.png)

3、先配置 JDK 和 Git。点击：Manage Jenkins>>Global Tool Configuration

![](/img/j/3.png)

![](/img/j/4.png)

选择 JDK，别名随便填，JAVA_HOME 填写查询到 jdk 的路径

![](/img/j/5.png)

选择 Git，Name 随便填 e 填写 2.2 查询到 git 的路径，配置完成后点击应用，在点击保存。

![](/img/j/6.png)

### 安装插件

安装插件，点击 Manage Jenkins>>Manage Plugins，点击可选插件

![](/img/j/7.png)

![](/img/j/8.png)

安装 Gitee 插件，找到可选插件 tab，搜索 gitee
![](/img/j/9.png)

安装 Maven 插件
![](/img/j/10.png)

安装 Git Parameter Plug-In 插件，用于添加 git 参数
![](/img/j/11.png)

安装 Environment Injector 插件，搜索 inject，此插件可以在 shell 脚本中可以使用 $a、$b 等自定义环境变量
![](/img/j/12.png)

安装 Publish over SSH 插件
![](/img/j/13.png)

#### 必须要配置 name 和 email，为了让每一次提交的代码都能配置到用户

```cmd
git config --global user.name "jenkins_git"
git config --global user.email "wuqi_y@163.com"
```

生成证书 绑定 gitee 或者 github

## SSH 公钥

```
# 生成ssh连接所需的证书
ssh-keygen -t rsa -C "wuqi_y@163.com"
```

### 将证书配置到 git 上。

登录 github 或 gitee，这里我以 gitee 为例，步骤如下：
   登录并进入 gitee 个人设置 – 点击“SSH 公钥”侧边栏 – 输入标题 – 黏贴刚才在 linux 上生成 id_rsa.pub 文件内容后保存。

### 添加 Gitee 配置（Manage Jenkins>>Configure System>>Gitee 配置）

![](/img/j/14.png)

![](/img/j/15.png)

![](/img/j/16.png)

![](/img/j/17.png)
![](/img/j/18.png)
![](/img/j/19.png)
![](/img/j/20.png)
![](/img/j/21.png)
可根据自己需要更改(记得安装 Node 哦)

```cmd
# 在执行过程中若遇到使用了未定义的变量或命令返回值为非零，将直接报错退出
set -eu
echo "<-------------------------------------->"
node -v
echo "安装依赖"
npm install

echo "<-------------------------------------->"
echo "打包出dist文件夹"
npm run build

# 先删除nginx下的旧数据
sudo rm -rf /www/wwwroot/test-jenks/*
# 再将新数据拷贝到nginx下
sudo cp -r dist/* /www/wwwroot/test-jenks/
```

最后执行即可
![](/img/j/22.png)
