---
title: VS Code 配置 C&C++ 开发环境
date: 2023-11-22 22:25:00
categories: Development & Progarmming
tags: C VSCode Windows WSL GCC MinGW
index_img: https://pixiv.re/.jpg
banner_img: https://pixiv.re/.jpg
---

# Windows or WSL ( Windows Subsystem for Linux )

在 Windows 上使用 VScode 进行 C 的开发主要有两种策略，一种是将编译器安装在 Windows系统中的 VSCode + MinGW 组合，另一种是将编译器安装在Windows Linux子系统 (也就是 WSL ) 中的 VSCode + WSL + GCC&G++ 组合。

# Visual Studio Code 的安装与初步配置

## 安装 Visual Studio Code

首先你要做的第一件事应该是下载 VSCode

使用浏览器搜索 `Visual Studio Code` ，或点击下方链接选择适合的版本进行下载，Windows 64位系统下载最左侧 Windows 大类下的 User Installer x64 即可；

[Download Visual Studio Code](https://code.visualstudio.com/download)

![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_1.png)

安装时碰到这个界面建议全部勾选；

![github](https://mirror.ghproxy.com/https://github.com/NanodaOvO/PictureHost/blob/main/vsc-c&c++_2.png)

安装完毕建议重启电脑以确保环境变量成功添加。

## 设置简体中文

初次进入 VSCode 时我们的界面是纯英文的，这时候在左侧的工具栏中找到![local](/2023-11-22_3.png)按钮或直接输入 `Ctrl+Shift+X` 打开扩展安装页，在搜索栏输入 `chinese` ，选择下载量最高的简体中文包，在介绍页点击 `Install` 等待安装完成，重启就可以了。

# VSCode + MinGW

我们首先来讲步骤相对较少的 VSCode + MinGW 组合。

## 安装 MinGW

