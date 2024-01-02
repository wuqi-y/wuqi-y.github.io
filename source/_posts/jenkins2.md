---
abbrlink: ''
comment: true
cover: true
date: '2023-08-23 11:33:00'
recommend: true
categories:
- 运维
tags:
- 运维
- 前端
title: Jenkins如何自动化部署前端项目(2)
updated: Sat, 26 Aug 2023 16:22:26 GMT
---
### Jenkins如何自动化部署前端项目

前置步骤我们都操作完了，这篇开始介绍jenkins的是哟。话不多说，看操作(没安装的请看我主页有详细的安装教程)

1、登录进入jenkins后会让你选择安装插件，选择第一个默认的就行。

2、配置JDK和Git都需要执行路径，所以需要先把执行路径找到，先进入服务器的终端界面执行

> JDK的路径

```
 echo $JAVA_HOME
```

如果是空记得先去设置java的环境变量 `which java` 查看java的安装路径

![jdk路径](/medias/j/1.png)

> Git的路径

```
 which git
```

![git路径](/medias/j/2.png)

3、先配置JDK和Git。点击：Manage Jenkins>>Global Tool Configuration

![](/medias/j/3.png)

![](/medias/j/4.png)

选择JDK，别名随便填，JAVA_HOME填写查询到jdk的路径

![](/medias/j/5.png)

选择Git，Name随便填e填写2.2查询到git的路径，配置完成后点击应用，在点击保存。

![](/medias/j/6.png)

### 安装插件

安装插件，点击Manage Jenkins>>Manage Plugins，点击可选插件

![](/medias/j/7.png)

![](/medias/j/8.png)

安装 Gitee 插件，找到可选插件tab，搜索gitee
![](/medias/j/9.png)

安装 Maven 插件
![](/medias/j/10.png)

安装 Git Parameter Plug-In 插件，用于添加git参数
![](/medias/j/11.png)

安装 Environment Injector 插件，搜索 inject，此插件可以在shell脚本中可以使用 $a、$b等自定义环境变量
![](/medias/j/12.png)

安装 Publish over SSH 插件
![](/medias/j/13.png)


#### 必须要配置name和email，为了让每一次提交的代码都能配置到用户

```cmd
git config --global user.name "jenkins_git"
git config --global user.email "wuqi_y@163.com"
```

生成证书 绑定gitee或者github

## SSH公钥

```
# 生成ssh连接所需的证书
ssh-keygen -t rsa -C "wuqi_y@163.com"
```

### 将证书配置到git上。

  登录github或gitee，这里我以gitee为例，步骤如下：
  登录并进入gitee个人设置 – 点击“SSH公钥”侧边栏 – 输入标题 – 黏贴刚才在linux上生成id_rsa.pub文件内容后保存。

### 添加Gitee配置（Manage Jenkins>>Configure System>>Gitee 配置）

![](/medias/j/14.png)

![](/medias/j/15.png)

![](/medias/j/16.png)

![](/medias/j/17.png)
![](/medias/j/18.png)
![](/medias/j/19.png)
![](/medias/j/20.png)
![](/medias/j/21.png)
可根据自己需要更改(记得安装Node哦)

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
![](/medias/j/22.png)
