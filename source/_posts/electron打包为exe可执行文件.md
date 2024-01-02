---
abbrlink: ""
categories:
  - - 前端
cover: https://s11.ax1x.com/2023/12/27/pibq0Nq.jpg
date: 2023-12-28 11:33:00
recommend: ""
swiper: ""
tags:
  - electron
title: electron打包为exe可执行文件
updated: 2023-12-26T10:10:19.264+8:0
---

### electron 打包为 exe 可执行文件

我们都知道使用 electron 时打包后会形成一个目录，目录中有很多文件

例如：

![原来的](https://s11.ax1x.com/2023/12/25/piH57b6.md.png)、

这样我们做完后就很不方便分享给别人，那如何把 `electron`打包后的代码打包为一个.exe 可执行文件呢？😵

这里我们采用 Inno Setup 把文件打包为一个可执行文件

首先在官网下载最新版本 [Inno Setup](https://jrsoftware.org/isdl.php)

或者点击 [这里 ](https://jrsoftware.org/download.php/is.exe)直接下载 🐷

然后下载对应系统版本

安装完成后新建项目然后删除代码替换如下

```c#
[Setup]
;生成的.exe名字
#define AppName "测试测试"
;你需要执行的exe的名字
#define buildAppName "app"

;这是app的名字
AppName=AppName
AppVersion=1.1
;每次安装打开目录
DisableDirPage=no
;输出的默认名字  默认安装目录（C:\Program Files (x86)\testapp）
OutputBaseFilename=testapp2
;打包到的文件夹目录
OutputDir=D:\test-electron
DefaultDirName={commonpf}\testapp999
;打包的exe图标目录
SetupIconFile=D:\test-electron\test.ico

[Files]
;需要添加的文件
Source: "D:\test-electron\app-win32-x64\*"; DestDir: "{app}"; Flags: recursesubdirs

;自动生成桌面快捷方式
[Icons]
Name: "{commondesktop}\{#AppName}"; Filename: "{app}\{#buildAppName}.exe"
Name: "{commonstartmenu}\Programs\{#AppName}"; Filename: "{app}\{#buildAppName}.exe"

;安装完自动打开
[Run]
Filename: "{app}\{#buildAppName}.exe"; Flags: postinstall nowait


[Code]
var
  CustomInstallPath: string;

function GetCustomInstallPath(DefaultPath: string): string;
begin
  if CustomInstallPath <> '' then
    Result := CustomInstallPath
  else
    Result := DefaultPath;
end;
```

然后点击菜单栏的 **Build** 然后点击 Compiler 等待打包成功即可了！🤗

![示例图](https://s11.ax1x.com/2023/12/26/pibiJAO.png)

![piH5v2d.png](https://s11.ax1x.com/2023/12/25/piH5v2d.png)
