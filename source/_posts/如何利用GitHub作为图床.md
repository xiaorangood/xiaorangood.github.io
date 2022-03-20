---
title: 如何利用GitHub作为图床
date: 2022-03-20 20:24:00
tags:
---

## 下载PicGo
进入[PicGo的下载地址](https://github.com/Molunerfinn/PicGo/releases)，根据系统选择版本。因为我的点好是 win11，因此选择的软件版本是` PicGo-Setup-2.3.0-x64.exe`。下载完成后，双击软件按照默认设置安装。

## 创建 GitHub 仓库
创建后，在我的GitHub页面中，就有一个 myImage 的仓库。
```
https://github.com/xiaorangood/myImage.git
git@github.com:xiaorangood/myImage.git
```

## 生成 token
点击“头像”->"setting" -> "Developer settings" -> "Personal access tokens" -> "Generate New token"。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_20-43-09.png" style="zoom:70%"/>

设置token的名字、有效期；并勾选“repo”，最后下拉到最下方，点击“Generate token”按钮。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_20-43-30.png" style="zoom:75%"/>


## 配置picgo
打开picgo软件，在左边的栏目中点击“图床设置” -> "GitHub图床"。按照下面的说明设置

- 设定仓库名：按照`用户名/图床仓库名`的格式填写
- 设定分支名：`master`
- 设定Token：粘贴之前生成的Token
- 指定存储路径：填写想要储存的路径，如`images/`，这样就会在仓库下创建一个名为 images 的文件夹，图片将会储存在此文件夹中。
- 设定自定义域名：它的的作用是，在图片上传后，PicGo会按照`自定义域名+上传的图片名`的方式生成访问链接，放到粘贴板上，因为我们要使用jsDelivr加速访问，所以可以设置为`https://cdn.jsdelivr.net/gh/用户名/图床仓库名`。jsDelivr的参考格式:`https://cdn.jsdelivr.net/gh/xiaorangood/myImage`

上述的内容填写完成后，点击“确认”按钮，再设置**GitHub图床为默认图床**。
<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/20220320212009.png" style="zoom:85%"/>

## 上传图片

点击左侧栏目里的上传区后，将需要上传的图片拖入上传区即可。