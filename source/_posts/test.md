---
title: markdown语法~~教学~~测试
date: 2023-10-12 12:00:00
updated: 2023-10-15 09:00:00
categories: test
tags: 
---

先把正版教程放在前面 [markdown官方教程](https://markdown.com.cn/basic-syntax)

<h1 align="center">⚠⚠⚠WARNING!!!!你需要通过下载VScode和Typora来获取阅读本文的权限！⚠⚠⚠</h1>

[安装VScode](https://code.visualstudio.com/ "世界上最好的代码编辑器")

如果你选择VScode作为你的markdown编辑器，请先记住这套快捷键：`Ctrl+K V` ，即先按 `Ctrl+K` ，然后放掉，紧接着再按 `V`，可以调出实时预览框，这能为你节省不少精力。

[安装Typora](https://www.typora.io/ "即时渲染，简洁快捷的markdown编辑器")

界面清新简洁的Typora是一款付费软件，若你没有能力购买正版，可以下载 [学习版文件](https://pan.baidu.com/s/1gH7LD5FELf-jpb49UxYcwQ?pwd=a3zi)，直接将下载得到的.dll文件粘贴至Typora文件夹目录即可。

# 基本语法

## 代码语法，强调语法の应用

如果我们需要强调什么，那么在需要强调的文字前面和后面分表加上`**`就可以了哦
例：我喜欢玩**原神**

我们可以用反引号😫,对就是那
个波浪线下面
的小玩意😖，你懂
的，来框住这
些可爱的
小字母们`chkdsk`
它们真可爱😍，不是么😌
如果你不喜欢也没事哦天哪
我的上帝我已经等不及要看看这美
丽的围栏代码块了🤗

``` c
include <stdio.h>
int main(){
    printf("hello world\n");
    return 0;
}
```

## 列表语法の运用

- ### 脂质
    1. 脂肪:细胞内良好的储能物质；是一种很好的绝热体，皮下的脂肪层起到保温作用；分布在内脏周围的脂肪具有缓冲和减压作用，保护内脏器官
    2. 磷脂:构成细胞膜及多种细胞器膜的重要成分
    3. 固醇
        - 胆固醇:构成动物细胞膜的重要成分，在人体内参与血液中脂质的运输
        - 性激素:促进人和动物生殖器官的发育及生殖细胞的形成
        - 维生素D:进人和动物肠道对钙和磷的吸收
        - 皮质醇
        - 醛固酮

- ### 糖类
    - 单糖
        - 葡萄糖
        - 果糖
        - 半乳糖
        - 核糖
        - 脱氧核糖
    - 二糖
        - 蔗糖
        - 乳糖
        - 麦芽糖
    - 多糖
        - 糖原
        - 淀粉
        - 纤维素
        - 肽聚糖（细菌细胞壁主要成分）

- ### 生态系统的四大原理
    -自生
    -协调
    -循环
    -整体
- ### 生态系统的功能
    - ##### 生态系统的主要功能
        - 物质循环
        - 能量流动
    - 信息传递

## 链接语法的应用
这是我的bilibili个人主页：[NanodaOvO](https://space.bilibili.com/287889648)
这也是我的bilibili个人主页（记得悬停鼠标指针！）：[NanodaOvO](http://space.bilibili.com/287889648 "这里住着一个废物")
这还是我的bilibli个人主页：<http://space.bilibili.com/287889648>
让我们小小地强调一下）
这是我的bilibili个人主页：**[NanodaOvO](https://space.bilibili.com/287889648 "这里住着一个废物")**
这也我的bilibili个人主页：[`NanodaOvO`](https://space.bilibili.com/287889648 "这里住着一个废物")

嘿，我是说，你还没有安装[VScode](https://code.visualstudio.com/)吗？快去下载！

## 分隔符语法の应用
很不巧，如果你是一个狂热的奇特分隔符爱好者，那么这里或许不太适合你

这是第一行，下面是我们亲爱的分隔符，3个以上的`*`就行了，加空格也可以

*     *      *

哦不喜欢星号么，那我们用`-`也可以哦，需要3个以上的`-`，加空格也可以

---

下划线也是一样3个以上的`_`

_ _  _   _

嘿，我的下划线到这就结束啦

## 转义符语法の应用

能当做转义符的符号太多了，建议直接阅读[markdown官方教程](https://markdown.com.cn/basic-syntax/escaping-characters.html "正版教程，童叟无欺")
我们只介绍一个`\`吧,`\`要紧挨着正文，不可以加空格！
\**强调**了吗？如来嘛；
他真\ **强调**了吗？真来了！

## 引用、换行、段落语法の的应用

> 远看是只狗🐶，近看是只若沫郭🐒。——迅鲁

是的只要空一行我们就可以开始下一段引用了😍，如果不空一行还会继续引用🥰，我觉得我们最好还是在每一段引用的前面和后面都空一行😘。
当然了在我们的正文需要分段&换行的时候同样需要空一行。

>创建段落，请使用空白行将一行或多行文本进行分隔。——markdown官方教程

除了段落，我们还要换行。我们除了按下两次enter之<br>外还有什么别的方法可以换行呢<br>看来加一个HTML的`<br>`标签就可以了呢

好，很有精神！下一个！

> when I see you again...ahhhhhhhhh,ahhhhhhhhhhh
>>谁问你了？☝️🤓
>>>我问了😋👌

哦闭嘴吧冰红茶，不然我就要用靴子👢狠狠踢你的屁股！😡

# 扩展语法

## 围栏代码块语法の应用

[参见上文](#代码语法，强调语法の应用)

## 表格语法の应用

   |      二维图位置         |政治左            |政治中               |政治右              |
   |      :---:        | :-               |       :-:          | -:                |
   |       上      |   社群主义        |    民主社会主义     |    施特拉瑟主义    |
   |       下      |   无政府资本主义   |   自由主义         |      纳粹主义      |

## 数学公式的应用

我们还是直接贴一些教程链接吧：

- [Markdown/LaTeX 数学公式和符号表](https://zhuanlan.zhihu.com/p/450465546)
- [[markdown语法]公式篇--整理总结了常用的公式语法全](https://blog.csdn.net/m0_37769093/article/details/107732606)
- [Markdown语言——数学公式](https://zhuanlan.zhihu.com/p/138532124)
- [使用Typora添加数学公式](https://blog.csdn.net/mingzhuo_126/article/details/82722455)
- [Typora数学公式汇总（Markdown）](https://zhuanlan.zhihu.com/p/261750408)

### 实例演示
$$
A^m_n = n(n-1)(n-2)(n-3)...(n-m+1) = \frac{n!}{(n-m)!}
$$

$$
C^m_n = \frac{A^m_n}{A^m_m} = \frac{n(n-1)(n-2)(n-3)...(n-m+1)}{m!} = \frac{n!}{m!(n-m)!}
$$

## 在markdown中添加emoji

>你知道吗，使用 [Typora](https://www.typora.io/) 时你可以直接向正文 中添加emoji，所以快去用 [Typora](https://www.typora.io/) 吧。——沃兹基硕德

好吧😂其实只要使用微软自带的输入法的就你就可以添加emoji了😍我来教你😝先切换到微软输入法，随便按一个字母，悬浮的备选栏这时候应该已经跳出来了，把你的视线往右移，按一下倒数第二个键，好了，现在你可以在markdown中输入emoji了😊

或者，你直接随便找个emoji网站复制一下不就行了嘛♥: [EMOJIALL](https://www.emojiall.com/zh-hans)