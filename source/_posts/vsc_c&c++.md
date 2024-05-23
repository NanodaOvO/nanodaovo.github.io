---
title: 在 Windows 上 使用 VS Code 配置 C&C++ 开发环境
date: 2023-11-22 22:25:00
updated: 2024-05-23 19:03:00
categories: Development & Progarmming
tags: C VSCode Windows WSL GCC Clang MinGW
index_img: https://pixiv.nl/49360261.jpg
banner_img: https://pixiv.nl/49360261.jpg
---

# Windows or WSL ( Windows Subsystem for Linux )

在 Win 上用 VScode 写 C 我推荐两种方案，一种是在 WSL 上操作，另一种就是直接把编译器装 Windows 上（MinGW）。

## VSCode + WSL + GCC/Clang

安装可能较为繁琐，但编程体验更好

### 为什么选择 WSL

我觉得好用😎

### 如何编译出文件在 Windows 上运行

交叉编译

可以必应搜索教程或者直接看我的下文教程。

### 启用 WSL 和虚拟化

方法一：直接在「启用或关闭 Windows 功能」中打开「适用于 Linux 的 Windows 子系统」和「虚拟机平台」

方法二：在「终端管理员」中输入如下代码；

``` PowerShell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

建议重启电脑确保成功打开。

### 更新 WSL

终端输入

版本检查：`wsl --version`，WSL1需要升级至WSL2

版本更新：`wsl --update`，已经是WSL2就不需要更新

也可以 [点击这里下载 WSL 更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

将 WSL2 设置为默认版本：`wsl --set-default-version 2`

### 在 WSL 上安装你想要的 Linux 发行版

> [微软官方教程：如何使用 WSL 在 Windows 上安装 Linux](https://learn.microsoft.com/zh-cn/windows/wsl/install)

#### 微软商店安装

适合对Linux一无所知的小白，建议安装Ubuntu（WSL），直接在微软商店搜索Ubuntu，直接安装就可以了，安装完后可能会弹出一个终端让你设置账号密码，不要关闭，后面还有用。

终端输入

查看安装版本：`wsl --list --verbose` / `wsl -l -v`

#### 终端手动安装（PowerShell）

终端输入

一键启用运行 WSL 并安装默认的 Linux 发行版：`wsl --install`

默认情况下，安装的 Linux 分发版为 Ubuntu。 可以使用 `-d` 标志进行更改。

- 若要更改安装的发行版，请输入：`wsl --install -d <Distribution Name>`。 将 `<Distribution Name>` 替换为要安装的发行版的名称。
- 若要查看可通过在线商店下载的可用 Linux 发行版列表，请输入：`wsl --list --online` / `wsl -l -o`。
- 若要在初始安装后安装其他 Linux 发行版，还可使用命令：`wsl --install -d <Distribution Name>`。

Windows11 或更高版本可以直接使用 `wsl --install <Distribution Name>` 安装其他可用的发行版

``` PowerShell
NAME                                   FRIENDLY NAME
Ubuntu                                 Ubuntu
Debian                                 Debian GNU/Linux
kali-linux                             Kali Linux Rolling
Ubuntu-18.04                           Ubuntu 18.04 LTS
Ubuntu-20.04                           Ubuntu 20.04 LTS
Ubuntu-22.04                           Ubuntu 22.04 LTS
Ubuntu-24.04                           Ubuntu 24.04 LTS
OracleLinux_7_9                        Oracle Linux 7.9
OracleLinux_8_7                        Oracle Linux 8.7
OracleLinux_9_1                        Oracle Linux 9.1
openSUSE-Leap-15.5                     openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4    SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5           SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed                    openSUSE Tumbleweed
```

比如输入 `wsl --install -d Debian` 就可以在 WSL 中安装 Debian 了。

#### 配置账户密码

>[微软官方教程：设置 Linux 用户名和密码](https://learn.microsoft.com/zh-cn/windows/wsl/setup/environment#set-up-your-linux-username-and-password)

使用“开始”菜单打开你安装的该发行版（默认情况下为 Ubuntu）。 系统将要求你为 Linux 发行版创建“用户名”和“密码”。

- 此用户名和密码特定于安装的每个单独的 Linux 分发版，与 Windows 用户名无关。
- 请注意，输入密码时，屏幕上不会显示任何内容。 这称为盲人键入。 你不会看到你正在键入的内容，这是完全正常的。
- 创建用户名和密码后，该帐户将是分发版的默认用户，并将在启动时自动登录。
- 此帐户将被视为 Linux 管理员，能够运行 `sudo` (Super User Do) 管理命令。
- 在 WSL 上运行的每个 Linux 发行版都有其自己的 Linux 用户帐户和密码。 每当添加分发版、重新安装或重置时，都必须配置一个 Linux 用户帐户。

若要更改或重置密码，请打开 Linux 发行版并输入命令：`passwd`。 系统会要求你输入当前密码，然后要求输入新密码，之后再确认新密码。

如果忘记了 Linux 分发版的密码：

1. 请打开 PowerShell，并使用以下命令进入默认 WSL 分发版的根目录：`wsl -u root`
2. 如果需要在非默认分发版中更新忘记的密码，请使用命令：`wsl -d <Distribution Name> -u` root，并将 `<Distribution Name>` 替换为目标分发版的名称。
3. 在 PowerShell 内的根级别打开 WSL 发行版后，可使用此命令更新密码：`passwd <username>`，其中 `<username>` 是发行版中帐户的用户名，而你忘记了它的密码。
4. 系统将提示你输入新的 UNIX 密码，然后确认该密码。 在被告知密码已成功更新后，请使用以下命令在 PowerShell 内关闭 WSL：`exit`。


如果你~~故意~~不小心跳过了系统自动弹出的账户密码配置终端，那用户名将会默认为 `root`，密码为空，也挺不错的，不是么？


### 安装编译器：GCC or Clang

GCC（GNU Compiler Collection）：兼容性好，使用范围更广，拥有更多教程示例，Linux 平台下的默认 C/C++ 编译器

Clang（LLVM's C Language Family Frontend）：运行速度更快，占用内存少，诊断信息可读性强，模块化架构拓展性强

相对来说 GCC 更适合新人上手，相比 clang，你所能查找到的关于如何配置 GCC 环境的教程也更多，推荐先安装 GCC，日后在考虑是否使用 Clang。

#### GCC

``` Linux Shell
sudo sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list  #切换阿里云镜像
sudo apt update -y  #更新软件包清单
sudo apt upgrade -y  #升级软件包
sudo apt-get install build-essential gdb clangd  #build-essential中包含gcc和一系列会用到的相关工具和库
```

验证安装

``` Linux Shell
whereis gcc g++ gdb clangd
```

#### Clang

``` Linux Shell
sudo sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list  #切换阿里云镜像
sudo apt update -y  #更新软件包清单
sudo apt upgrade -y  #升级软件包
sudo apt-get install clang clangd lldb cmake
```

验证安装
``` Linux Shell
whereis clang clangd lldb cmake
```

### 安装 VSCode

[Download Visual Studio Code](https://code.visualstudio.com/download) ，选择适合自己电脑的版本，安装时碰到「选择附加任务」界面直接全部勾选，安装完毕建议重启电脑以确保环境变量成功添加。

>[为什么要添加环境变量？](https://zhuanlan.zhihu.com/p/547720085)

### 安装 VSCode 插件

请根据自身体验选择合适的插件：

 - Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code
   - 英语废渣的福音，用英文界面更能锻炼英语能力哦
 - WSL
   - 提供对 WSL 的支持
 - C/C++ & C/C++ Extension Pack
   - 可以生成 .vscode 目录的配置文件，使各种命令行工具可以在 VSCode 的图形化界面中使用，自身拥有基础的报错、跳转、代码补全功能
   - 点击界面右上角的小三角可以看到「到运行 C/C++ 文件」和「调试 C/C++ 文件」的功能；可以帮助你快速生成配置文件以调试运行
 - clangd
   - 拥有强大的静态检查功能
   - 安装过程中弹出 clangd Extension 和 C/C++ Extension 的 IntelliSense 冲突的时候请选择关闭 IntelliSense
   - 插件不能独自完成代码分析，需要在 Linux 系统中安装 clangd 包，自动下载如果卡住了需要科学上网或是直接在终端中使用 `sudo apt-get install clangd` 命令，具体教程请阅读 [clangd官方文档](https://clangd.llvm.org/installation)
   - Windows 下安装需要使用 MSYS2，较为繁琐，所以为了方便地使用 clangd 建议还是用 WSL 吧
 - Code Runner
   - 更好的代码运行
 - C/C++ Runner
   - 更好的代码调试，不调试的可以略过
 - CodeLLDB
   - C/C++ Runner的前置依赖
   - 对 lldb 调试器提供支持
 - C/C++ Snippets
   - 代码模板，预制菜
 - CMake
   - 大一C语言基本上只涉及单文件编程，不怎么用的到，可以顺带装上
 - VSCodeSnap
   - 代码截图插件，比普通截图更美观，“我求求你们不要拍屏了”

## VSCode + Windows + MinGW

我们最后再来讲步骤相对较少的 VSCode + MinGW 组合，MinGW 的体验其实挺烂的，如果你只是想要 VSCode 的编程体验可以凑合凑合。

VSCode和插件部分请参照上文，咕~
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

如果没成功可以试试重启电脑哦咕


