---
title: Noob C 外传：令人忍俊不禁 —— 笑点解析之 VS Code + MinGW
date: 2024-05-31 15:48:00
updated: 
categories: Share & Misc
tags: C VScode MinGW
index_img: https://pixiv.nl/.jpg
banner_img: https://pixiv.nl/.jpg
---

## 前言

本文是笔者面向纯小白的编程教程 Noob C 系列的外传，关于如何配置 MinGW 环境的教学。其实本来这部分是和 WSL 一起讲的，结果越讲越混，感觉还是单独拿出来好了。

下面是教程全集链接：

- [Noob C 其一：为什么我使用 Visual Studio Code](https://nanodaovo.github.io/2023/11/21/vsc_rec/)
- [Noob C 其二：在 Windows 上 使用 VS Code 配置 C&C++ 开发环境](https://nanodaovo.github.io/2023/11/22/vsc_c&c++/)
- [Noob C 其三：使用 VS Code 开始编写 C&C++ 代码](https://nanodaovo.github.io/2024/05/23/vsc_c&c++_startcoding/)
- Noob C 外传：令人忍俊不禁 —— 笑点解析之 VS Code + MinGW（本教程）

## VS Code + Windows + MinGW

MinGW 的体验其实挺烂的，如果你只是想要 VS Code 的编程体验可以凑合凑合。

VS Code的安装和操作请参照教程前文。

### 安装 MinGW

~~PVP~~大佬可以访问 [MinGW官网](https://www.mingw-w64.org/downloads) 选择适合你的版本，小白可以直接跟着我的步骤下：

 - 访问 https://github.com/niXman/mingw-builds-binaries/releases
 - 32位系统安装 i686-13.2.0-release-posix-dwarf-ucrt-rt_v11-rev0.7z
 - 64位系统安装 x86_64-13.2.0-release-posix-seh-ucrt-rt_v11-rev0.7z

文件名里的 13.2.0 是版本名，你下载更加新的版本也可以，截至我截稿的时候反正最新版还是 13.2.0 ；下载完安装包并解压后，把解压好的文件夹找个合适的地方放起来，别放在**桌面**或者**下载**里，那样你可能会随手删掉的。

接下来是很重要的一步，添加名为 (PATH) 的环境变量，如果你想了解环境变量的作用，建议先阅读下文；

### 添加环境变量

在任务栏的搜索框直接搜，直接在屏幕下方任务栏的搜索框中输入 `path` ，在弹出的选项中就可以进入编辑环境变量页面。至于多记几种方法也没什么用，你只要知道环境变量很重要，想不起来的时候去bing搜一下就行了。

在弹出的窗口中找到 **环境变量** 按钮，双击用户变量或是系统变量中的 `Path` 变量，选择新建变量，将你解压出来的文件夹中 `\bin` 文件夹的完整路径填写到文本框中并保存就可以了。你可以使用如下命令验证mingw是否成功添加了环境变量：

``` PowerShell
gcc --version
g++ --version
```

如果没成功可以试试重启电脑。