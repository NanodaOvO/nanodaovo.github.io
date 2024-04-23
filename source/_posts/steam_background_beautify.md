---
title: Steam个人资料背景美化教程
date: 2024-03-19 16:50:00
updated: 
categories: Share & Misc
tags: Steam Background
Front-matter: False
index_img: https://pixiv.nl/.jpg
banner_img: https://pixiv.nl/.jpg
---

### 前言

最近做Steam个人资料美化的时候遇到了一些问题，决定自己搓一篇心得.

本文只介绍了「精选艺术作品展柜」&「我的创意工坊展柜」，请记住这两个展柜的名字，以便你能在个人资料里正确地选择展柜.

## 精选艺术作品展柜 ——「一张完整的图」

通常放置在所有展柜的最上方，通过融入背景达到美化的效果；如果打算在下方也使用精选艺术作品展柜，相信看完下面的内容你也能举一反三.

在Steam于 2021-01-12 更新了「精选艺术作品展柜」之后，传统二分型的「艺术作品展柜」的功能已经基本上被替代，我接下来也不会再介绍这种方法.（懒）

精选艺术作品展柜的效果如下：

![](https://mirror.ghproxy.com/https://raw.githubusercontent.com/NanodaOvO/PictureHost/main/steam_background_beautify_1.png)

### 获取裁剪好的图片

首先你得有拥有 **一整张** 裁剪好的背景图片，动的静的都行，静态的相对比较简单，动态的步骤较多.

#### 获取静态图片

1. Steam库存 -> 高级筛选 -> 个人资料背景 -> 查看完整大小 -> 复制弹出的浏览器页面中的网页URL
2. 访问 [steam.design](steam.design) ，在「Paste a Background URL Here」输入框中粘贴你的背景URL
3. 下载并解压包含裁剪好的图片的压缩包，记得选那张宽度比较大的

#### 获取动态图片

1. Steam个人资料 -> 右击背景处选择复制网页URL -> 复制到浏览器地址栏中打开个人资料界面
2. 右键背景选择「将视频另存为」，保存下来的视频是 webm 格式，存在你找的到的地方就行
3. webm 转 GIF 网站：[convertio.co/zh/webm-gif](https://convertio.co/zh/webm-gif/)
4. 裁剪图片为完美贴合精选艺术作品展柜的大小：访问 [ezgif.com](https://ezgif.com/) ，选择 `crop` 工具，选择你上一步转换好的 GIF 文件上传；裁剪的参数为 `L:495,T:256,W:630,H:824`，裁剪并保存图片至本地；不要急着关掉网页，待会还可以用这个网站往你的gif上加点别的东西；

### 在裁剪好的图片上添加其他内容

Steam艺术作品上传的大小上限为 **5MB** ，请确保你最终的成品大小小于 5MB.

#### 静态图片处理

使用任意的图片处理软件直接编辑你裁剪好的静态图片即可.

#### 动态图片处理

回到刚才的 [ezgif.com](https://ezgif.com/) ，找到你刚刚裁剪过的 GIF「Cropped image」，选择 `overlay` 工具，上传你裁剪好的素材图片，点击一次上传就可以了，网站加载预览的速度比较慢，请耐心等一会；合成好的图片通常会很大，在网站上找到 `optimize` 工具，压缩至 5MB 以下就可以得到最终的成品了。

### 上传图片

在网页版 Steam [上传艺术作品](https://steamcommunity.com/sharedfiles/edititem/767/3/) ，选择图片并上传，我知道你很想点保存并继续 ~~但你先别急，让我先急~~

`F12` 打开控制台（safari 是 option + command + c）进入开发者工具，选择控制台（console），输入如下代码，修改图片宽高：

``` JS
$J('#image_width').val(1000).attr('id', '');
$J('#image_height').val(1).attr('id', '');
```

如果你想置空艺术作品的名称，可以输入如下代码：

``` JS
v_trim = _ => {
  return _;
};
$J('#title').val(' \n' + Array.from(Array(126), _ => '\t').join(''));
```

保存并上传，审核通过后在编辑个人资料中「已展示的展柜」选择「精选艺术作品展柜」即可.

## 我的创意工坊展柜 ——「五等分的 GIF」

展柜选择列表里还有名为「创意工坊展柜」的选项，只能精选一件任意创意工坊作品，你应该选择的是「我的创意工坊展柜」.

通常用来在个人资料里实现视频的播放，图片有截图展柜和艺术作品展柜作为更好的选择；

和制作动态背景一样需要将源素材转换为 GIF 格式.

### 获取 GIF

1. 准备好你要用到的视频，
2. 视频转 GIF 网站：[www.freeconvert.com/convert/video-to-gif](https://www.freeconvert.com/convert/video-to-gif)
3. 宽度 `Width (px)` 设置为 `630` ；裁剪起点、裁剪终点和帧率按需选择

### 五等分裁剪 GIF

1. 访问 [ezgif.com](https://ezgif.com/) ，选择 `crop` 工具
2. 拖动选取框使其上、左、下三面紧贴边沿；按 **126px** 的宽度五等分裁剪图片，`Left` 值依次为 `0` `126` `252` `378` `504`，即为 630/5 的倍数
3. 保存到本地，编号以便于辨别顺序

### 修改 GIF * 5 尾部十六进制值

1. 访问 [hexed.it](https://hexed.it/)
2. 将裁剪好的 GIF 直接鼠标拖进网站，将最后一位元素 `3B` 改成 `21` ，编好序号并保存
3. 五份都要改！记得去检查一下

### 上传 GIF * 5

还是在网页版 Steam [上传艺术作品](https://steamcommunity.com/sharedfiles/edititem/767/3/) 界面中选择图片，上传

`F12` 打开控制台（safari 是 option + command + c）进入开发者工具，选择控制台（console），输入如下代码，修改 gif 宽高，每次上传图片后都要输！

``` JS
$J('[name=consumer_app_id]').val(480);
$J('[name=file_type]').val(0);
$J('[name=visibility]').val(0);
```

如果你想置空艺术作品的名称，可以输入如下代码：

``` JS
v_trim = _ => {
  return _;
};
$J('#title').val(' \n' + Array.from(Array(126), _ => '\t').join(''));
```


## Q&A 常见问题

Q：为什么在使用 Edge 浏览器在第三步下载 gif 的时候，跳转到了一个叫「Edge Image Viewer」的界面里并且无法下载 gif 格式的动图？

A：大概率是 Edge 测试版的实验功能搞的鬼，在地址栏中输入 `edge://flags/` 进入实验功能，找到「Edge Image Viewer」并设置为 `DISABLED` 即可；改完设置建议把浏览器和电脑都重启一遍，确保设置生效.

---

Q：在 ezgif 上使用 `overlay` 工具时，我的素材图片无法调整到我想要的位置怎么办？

A：在 ps 中创建一个与裁剪好的 GIF 长宽比相等的模板，提前布置好所有需要用到的素材。直接使用其长宽 `630*824` 创建模板即可.

---

Q：为什么我的艺术作品在展示和选取界面是一条细细的黑线？

A：因为使用代码强制修改了图片的宽高，所以无法正常显示略缩图；不修改宽高值会导致图片无法适应整个展柜的大小，左右留有间距.






