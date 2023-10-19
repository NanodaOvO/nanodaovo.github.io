---
title: 从编译问题到历史包袱 —— undefined reference to 'sin'
date: 2023-10-19 22:25:00
categories: Debug
tags: C
index_img: https://pixiv.re/104146853.jpg
banner_img: https://pixiv.re/104146853.jpg
---

# 从编译问题到历史包袱 —— undefined reference to 'sin'

- 开发环境：WSL＋GCC＋VScode，Linux版本：Ubuntu 22.04.3


- 问题：使用 gcc 对引入 `math.h` 的 .c文件编译时出现 ``undefined reference to 'sin'`` 报错，编译过程中止

**原题如下**


已知三角形的两条边及其夹角，求该三角形的面积 （$ S= \frac{1}{2} a b sin \theta ，\theta  $ 为边 $a$ 和 $b$ 的夹角）

书上提供了一种简单易懂的计算方法，省略了让程序判断任意两边之和是否大于第三边的步骤，判断输入数据是否能组成三角形的过程全由输入者完成。

>当然也可以用海伦公式：$S = \sqrt {s(s-a)(s-b)(s-c)} ，s = \frac{a+b+c}{2}  ，s$ 为半周长。

```c
#include <stdio.h>
#include <math.h>

int main()
{
    float a,b,c,s;
    scanf("%f%f%f",&a,&b,&c);
    s = 1.0 / 2 * a * b * sin(3.14 / 180 * c);
    printf("%.2f\n",s);
    return 0;
}
```

意外的是，这段简单的代码并不能成功编译成可执行文件，无论我们用的是哪种方法来计算三角形的面积，只要在开头引入了 `math.h`，编译过程便无法完成。

当我在 VScode 内使用 GCC 进行调试时，终端的输出是这样的：

```
正在启动生成...
/usr/bin/gcc -fdiagnostics-color=always -g "/workshop/code-reproduction/2-11 三角函数.c" -o "/workshop/code-reproduction/2-11 三角函数"
/usr/bin/ld: /tmp/ccfgMBr3.o: in function `main':
/workshop/code-reproduction/2-11 三角函数.c:8: undefined reference to `sin'
collect2: error: ld returned 1 exit status

生成已完成，但出现错误。

 *  终端进程启动失败(退出代码: -1)。 
 *  终端将被任务重用，按任意键关闭。 
```

虽然一眼看上去字很多，但其中大部分都是目标文件的名称和路径这些无用信息，重要的提取其中的关键信息；

```
gcc -fdiagnostics-color=always -g "test.c" -o "test"
ccfgMBr3.o: in function `main':
test.c:8: undefined reference to `sin'
collect2: error: ld returned 1 exit status
```

- 第一行执行的正是 `gcc test.c -o test` 这一GCC编译全过程的简化代码

- 第二行输出，名为 `ccfgMBr3.o` 的二进制机器代码文件已经成功生成并被输入链接器，这说明编译过程的前三步：预处理、汇编、编译都没有问题；那问题只能是出在了第四步：**链接**

- **第三行的 `undefined reference to 'sin'`，也就是对 "sin" 的未定义引用**。我们可能会误以为我们引用了头文件，函数自然是**定义**在头文件里了，其实不然，函数的**定义**是由库文件完成的，而头文件只是对函数进行了**声明**，那找不到函数的**定义**，自然就是找不到相应的库文件了，而寻找库文件的工作是由链接器完成的，正好与上一点相呼应

正常思维下，我们并不应该需要通过 `-l` 来手动链接库文件，毕竟一个完整的c语言编译器都拥有链接标准库的功能，只有对于其他的库（例如非标准库、第三方库等），我们才需要我们进行手动链接，`math.h`是一种十分常见的头文件，对应的数学库 `libm.so` 也理所应当是标准库啊，为什么 GCC 没有默认链接数学库呢？

很显然，这并非是所有C语言编译器的通病。经过测试，MinGW、MSVC 都会默认链接 `math.h` 对应的数学库，然而 GCC 和 Clang 却没有默认链接数学库，事实上 GCC 只会默认链接 `libc.a` 或者 `libc.so`，这又是什么原因？

辗转知乎、C语言中文网、StackOverflow 等多个平台，我才逐渐意识到：这或许又是C语言的一个历史包袱。

在c语言面世的那个年代，浮点数计算(FPU)还不是标配，浮点计算代价高昂，在当时如果想使用数学计算, 需要CPU通过整数计算来模拟, 这种情况下计算效率非常低, 很多程序在编写的时候都会尽量避免使用浮点。不同的数学计算具有不同的取舍, 比如我希望计算要快，可以牺牲精确度，或者我希望足够精确, 慢点无所谓。如此可有可无的情况下也就不必将设计浮点运算的数学库作为标准库，所以也就不会默认链接数学库了。

当现代硬件性能突飞猛进地发展、浮点计算已不再困难时，已经没有什么必要要求编译器默认数学库了。有需要的人仍然可以会手动去链接它，对于那些用不到它的人，它还是一个不怎么用的到的库文件，毕竟现在方便进行数学计算的高级语言琳琅满目，谁会去用C语言算一个三角函数值呢？

从一个小小的编译问题开始，沿着一点一滴的线索，一硅一步地寻找，本以为能走出黑暗，最终迎接我的却是C语言家族的又一个历史包袱。C或许就是这样一门语言，缝缝补补，令人乏味。

## 最终的解决方案

打开源文件目录下的 `.vscode` 文件夹，打开 `tasks.json` ，在第10行和第11间额外添加一行，内容为 `"-lm",` ，其缩进与第10行和原第11行长度一致。效果如下

```
上略
                "${file}",
                "-lm",
                "-o",
下略
```

再次调试或运行的时候，就不会出现 ``undefined reference to 'sin'`` 的报错了。

感谢 [H2Sxxa](https://github.com/H2Sxxa) 在 Debug 过程中对本人提供的帮助。

## 参考资料

- [使用WSL来运行gcc配合VSCode进行C的开发](https://blog.h2sxxa.eu.org/2023/08/10/wsl-gcc-vscode/)
- [linux下解决c语言undefined reference to 'sin'](https://blog.csdn.net/mhhyoucom/article/details/19156481)
- [Linux下详解gcc编译过程（含代码示例）&& gcc使用教程](https://blog.csdn.net/weixin_47826078/article/details/120474122) 
- [Ubuntu添加math.h头文件编译的问题](https://blog.csdn.net/zhenguo26/article/details/79432140)
- ["undefined reference to XXX"问题总结](https://zhuanlan.zhihu.com/p/81681440)
- [MSVC、MINGW,gcc、g++,qmake、cmake的联系和区别](https://www.zhihu.com/question/333560253)
- [Linux的so文件到底是干嘛的？浅析Linux的动态链接库](https://www.zhihu.com/tardis/zm/art/235551437)
- [C语言头文件完全解析（连“#”我都给你讲明白）](https://blog.csdn.net/CRAZY_eyes/article/details/104868178)
- [彻底理解链接器：一，什么是链接器](https://zhuanlan.zhihu.com/p/369036368)
- [彻底理解链接器：二，符号决议](https://zhuanlan.zhihu.com/p/369039101)
- [C语言之链接知识](https://blog.csdn.net/u010650845/article/details/90413038)
- [在C语言中，math.h中定义的各种数学函数在电脑上具体是怎么实现的？](https://www.zhihu.com/question/21914131)
- [必须知道的C语言知识细节：声明和定义](https://zhuanlan.zhihu.com/p/162578969)
- [程序员应如何理解标准库](https://zhuanlan.zhihu.com/p/191613862)
- [GCC -l选项：手动添加链接库](https://c.biancheng.net/view/2382.html)
- [Why do you have to link the math library in C?](https://stackoverflow.com/questions/1033898/why-do-you-have-to-link-the-math-library-in-c)
- [gcc，clang在编译c程序时为什么不默认连接数学库？](https://www.zhihu.com/question/493038432)
- [关于编译：为什么必须在C中链接数学库？](https://www.codenong.com/1033898/)

题目来源：清华大学出版社 C语言程序设计(第三版) P.60 例题 2-11

