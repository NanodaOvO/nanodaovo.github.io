---
title: Noob C 其三：使用 VS Code 开始编写 C&C++ 代码
date: 2024-05-23 19:36:00
updated: 
categories: Development & Progarmming
tags: C Windows WSL GCC Clang VScode
index_img: https://pixiv.nl/118435208.jpg
banner_img: https://pixiv.nl/118435208.jpg
---

## 前言

本文是笔者面向纯小白的编程教程 Noob C 系列的第三章。许多新手在使用 VS Code 运行和调试代码的的时候都犯过难，吃过不少报错。本文会尽量简明地告诉你如何正确地进行调试和运行的操作，让你摆脱那个只会按 F5 的自己。

如果你还没有配置好C语言的编程环境，请先阅读教程的第二章。

下面是教程全集链接：

- [Noob C 其一：为什么我使用 Visual Studio Code](https://nanodaovo.github.io/2023/11/21/vsc_rec/)
- [Noob C 其二：在 Windows 上 使用 VS Code 配置 C&C++ 开发环境](https://nanodaovo.github.io/2023/11/22/vsc_c&c++/)
- Noob C 其三：使用 VS Code 开始编写 C&C++ 代码（本教程）
- [Noob C 外传：令人忍俊不禁 —— 笑点解析之 VS Code + MinGW](https://nanodaovo.github.io/2024/05/31/vsc_mingw)

## VS Code 核心概念 —— 工作区

工作区是一个具有独立设置和文件列表的容器。通过创建工作区，我们可以用于存储和组织相关的项目文件，并在其中进行开发工作。在 VS Code 中，打开一个文件夹会默认创建一个工作区。一个工作区可以包含一个或多个文件夹，这些文件夹可以位于不同的路径下。工作区会记录打开的文件列表、插件扩展、用户设置等信息。

以C语言为例，你前面装的 C/C++ 插件会为每个工作区生成一系列存储于 .vscode 目录中的配置文件（你也可以手动添加），具体功能我们下面会讲到，这些配置文件中的内容负责告诉 VS Code 调试、运行过程中每一步应该执行什么操作。所以，你应该确保每次编写C语言代码时使用的是同一个工作区，这样可以省去你多次配置的麻烦。

### VS Code 的 工作区(Workspace) 和 Visual Studio 的 项目(Project) 的区别

VS Code 中，工作区是指你打开的一个或多个文件的集合，这些文件可能属于同一个项目或不同的项目。工作区可以包含多个文件和文件夹，但它们并没有被组织成一个正式的项目结构。VS Code 的工作区更灵活，可以用于编辑任意类型的文件，不需要遵循特定的项目结构或配置。

Visual Studio 的项目是一个更为结构化的项目，通常包含一组相关的文件和文件夹，这些文件和文件夹按照一定的规则组织，支持特定的编程语言和开发框架。一个项目可以包含源代码文件、资源文件、配置文件等，并且通常会有一个项目文件（如.csproj、.sln等），用于定义项目的结构和设置。

如果你们的C语言老师让你们在使用 VS 时为每一个 .c 创建一个项目，那你在 VS Code 中就不需要这么做了！

## 基于指定工作区的 VS Code 的基本操作

在今后使用 VS Code 的过程中你可以自行探索 VS Code 的各种功能，养成自己的使用习惯，限于篇幅本文只在这里简短地介绍对于源代码 .c 文件最基础的管理方法。

打开 Windows 资源管理器，找到左侧目录中的「Linux」，选择你要用到 Linux 系统，在 `\root` 目录下新建一个文件夹，使用英文和数字命名，为了叙述方便，我先将其命名为 `workshop`。在 VS Code 界面左上角「文件」选项下选择打开文件夹，在弹出的地址栏中输入 `workshop` 的路径。鼠标光标移到左侧 VS Code 资源管理器栏时，右上角会显示四个小图标，第一个就是生成文件（也可以在空白处右键生成），重命名该文件为 `test.c`（没有资源管理器界面的鼠标左键点一下左侧一排按钮中的第一个就行了）。打开 `test.c` 随便输入一段代码：

``` C
#include "stdio.h"

int main()
{
    printf("hello world\n");
    return 0;
}
```

`Ctrl + S` 保存。我知道你已经等不及按 F5 了，~~但是你先别急~~你先看一下 F5 是什么功能。鼠标单击 VS Code 顶栏的「运行」就可以找到 F5 的功能：调试，进一步说，是根据你的默认配置进行调试。这里我们先抛开调试，先来试试编译运行功能。

## 如何运行C语言代码

### 在终端中输入指令编译运行（兼命令行教学）

以上面我们提到的 test.c 文件为例，在 VS Code 顶栏的「查看」栏中找到终端并打开，在终端中输入如下 Shell 命令，若成功在终端输出了 hello world 则为成功。

GCC 编译器输入：

``` Shell
cd "/root/test/" && gcc test.c -o test -lm && "/root/test/"test
```

这行指令的含义是：

1. 我们发现 VS Code 的终端是在默认的 `\root` 目录下打开的，所以我们先使用 `cd` 命令切换到当前 .c 文件所在的路径；
2. 然后，我们使用 GCC 编译器的命令，将 test.c 文件编译为可执行文件，其中 `-lm` 的作用是链接数学库，这么做原因可以看我的 [从编译问题到历史包袱 —— undefined reference to 'sin'](https://nanodaovo.github.io/2023/10/19/debug_mathh/)
3. 最后再直接运行可执行文件 test，在终端输出 hello world

Clang 编译器输入：

``` Shell
cd "/root/test/" && clang test.c -o test && "/root/test/"test
```

当然我们在 Windows Terminal 中打开 Linux 终端的效果也是一样的，Windows Terminal 是 Win11 系统就自带的终端程序，右键底边菜单栏徽标 -> 终端/终端管理员，在打开 PowerShell 的过程中就打开了 Windows Terminal。可以直接在 PowerShell 中输入 `<系统名>`，比如我安装的是 Ubuntu 就输入 `ubuntu` ，就可以进入 Linux 的 Shell 了；在 Windows Terminal 的标签栏上的下拉栏选择 Ubuntu 也可以直接打开一个新的 Linux Shell 界面，进入 Shell 后就可以输入上面的指令编译运行文件了。

> [Linux下的终端和shell概念](https://www.cnblogs.com/jplatformx/p/4366278.html)
> 
> [What's the difference between a console, a terminal, and a shell?](https://www.hanselman.com/blog/whats-the-difference-between-a-console-a-terminal-and-a-shell)
>
> 

限于篇幅我不可能列出所有的 Linux 和 Windows 命令，感兴趣的可以自行查找资料学习。

### 使用 Code Runner 插件进行编译运行（兼配置插件设置教学）

在界面右上角可以找到一个小三角形状的运行键，点击旁边的下拉栏，选择「 Run Code (Ctrl+Alt+N) 」就可以使用 Code Runner 快速地编译运行了。观察 VS Code 工作台的输出我们就可以知道 Code Runner 具体执行了什么命令。Code Runner的默认C语言编译器是 GCC，如果我们想要使用 Clang 或者自定义编译运行过程中的指令（比如链接数学库），就需要找到这个插件配置文件的所在。

- 左侧按键栏 -> 拓展 -> Code Runner -> 小齿轮 -> 扩展设置 -> Code-runner: Executor Map -> 在 settings.json 中编辑（配置插件设置的通解）

由此我们可以发现 Code Runner 插件的配置位于 VS Code 的用户全局配置文件 settings.json 中，你也有许多别的方法可以找到 settings.json 文件：

- C:\Users\<用户名>\AppData\Roaming\Code\User\settings.json 直接打开
- 左侧按键栏 -> 个人资料 -> 设置 —— settings.json
- 文件(F) -> 首选项 -> 配置文件(默认) -> 显示配置文件 -> 设置 —— settings.json
- 左下角齿轮设置 -> 配置文件(默认) -> 显示配置文件 -> 设置 —— settings.json

~~就是主打一个什么都教~~

在 settings.json 中找到 "code-runner.executorMap" 对象，找到对应的语言修改对应的指令即可。

###

## 如何调试C语言代码

### 对 .vscode 配置文件夹的初步认识

还记得你在新建 .c 文件时自动生成的 .vscode 文件夹吗？里面存放着你可以用到的 .json 配置文件。

例如 launch.json，它实际上就负责告诉 VS Code 你每次按下 F5 启动调试时应该如何执行。比如，可执行文件是应该生成在和 .c 源文件同一目录下，还是生成在一个指定的文件夹，比如 `\build` 下呢？应该用 GDB 作为调试器还是选择 LLDB 呢？这些都是你可以在配置文件中配置的。