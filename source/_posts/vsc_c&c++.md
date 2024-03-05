---
title: 在 Windows 上 使用 VS Code 配置 C&C++ 开发环境
date: 2023-11-22 22:25:00
updated: 
categories: Development & Progarmming
tags: C VSCode Windows WSL GCC MinGW
Front-matter: False
index_img: https://pixiv.nl/.jpg
banner_img: https://pixiv.nl/.jpg
---

# Windows or WSL ( Windows Subsystem for Linux )

在Windows上使用VScode进行C的开发主要有两种策略，一种是将编译器安装在Windows系统中的 VSCode + MinGW 组合，另一种是将编译器安装在Windows Linux子系统 (也就是WSL) 中的 VSCode + WSL + GCC&G++ 组合。

# Visual Studio Code 的安装与初步配置

## 安装 Visual Studio Code

首先你要做的第一件事应该是下载 **VSCode**

使用浏览器搜索`Visual Studio Code`，或点击下方链接选择适合的版本进行下载，Windows 64位系统下载最左侧 Windows 大类下的 **User Installer x64** 即可；

[Download Visual Studio Code](https://code.visualstudio.com/download)

![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_1.png)

安装时碰到这个界面建议全部勾选；

![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_2.png)

安装完毕建议重启电脑以确保环境变量成功添加。

## 设置中文

初次进入VSCode时我们的界面是纯英文的，这时候在左侧的工具栏中寻找![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_3.png)按钮或直接输入 `Ctrl+Shift+X` 打开扩展安装页，在搜索栏输入 `chinese` ，选择下载量最高的简体中文包，在介绍页点击`Install`，等待安装完成，重启VSCode就可以了。

如果你的Vscode界面仍然是英语，那你就用英语吧，我相信你一定是英语大神）

# VSCode + MinGW

我们首先来讲步骤相对较少的 VSCode + MinGW 组合。

## 安装 MinGW

~~PVP大佬~~ 你可以访问 [MinGW官网](https://www.mingw-w64.org/downloads) 选择适合你的版本，小白可以直接跟着我的步骤下：

 - 访问 https://github.com/niXman/mingw-builds-binaries/releases
 - 32位系统安装 i686-13.2.0-release-posix-dwarf-ucrt-rt_v11-rev0.7z
 - 64位系统安装 x86_64-13.2.0-release-posix-seh-ucrt-rt_v11-rev0.7z

文件名里的 13.2.0 是版本名，你下载更加新的版本也可以，截至我截稿的时候反正最新版还是 13.2.0 ；下载完安装包并解压后，把解压好的文件夹找个合适的地方放起来，别放在**桌面**或者**下载**里，那样你可能会随手删掉的。

接下来是很重要的一步，添加名为 (PATH) 的环境变量，如果你想了解环境变量的作用，建议先阅读下文；

>[为什么要添加环境变量？](https://zhuanlan.zhihu.com/p/547720085)

### 添加环境变量 (PATH) 的方法：

我用的最多的方法是在任务栏的搜索框直接搜，直接在屏幕下方任务栏的搜索框中输入 `path` ，在弹出的选项中就可以进入编辑环境变量页面。至于多记几种方法也没什么用，你只要知道环境变量很重要，想不起来的时候去bing搜一下就行了。

在弹出的窗口中找到 **环境变量** 按钮，双击用户变量或是系统变量中的 `Path` 变量
![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_4.png)
选择新建变量，将你解压出来的文件夹中 `\bin` 文件夹的完整路径填写到文本框中并保存就可以了。你可以使用如下命令验证mingw是否成功添加了环境变量：
```cmd,powershell
gcc --version
g++ --version
```
如果没成功可以试试重启电脑。

## 安装 VSCode 插件

关于下文没有推荐到的插件，请看 [VSCode插件使用报告 (1) ](https://nanodaovo.github.io/1145/19/19/vsc_plug-in_usage_report_1/)。





