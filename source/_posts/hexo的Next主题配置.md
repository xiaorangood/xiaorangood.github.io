---
title: hexo的Next主题配置
date: 2022-03-26 23:52:03
tags: 
    - 静态博客
    - hexo
    - Next主题
---

## 选择仓库

在设置主题时候，无意间发现Next是有两个库，名字很相像，名字与地址分别是：
- [theme-next/hexo-theme-next](https://github.com/theme-next/hexo-theme-next)
- [next-theme/hexo-theme-next](https://github.com/next-theme/hexo-theme-next)

next-theme的主题，是从v8.0.0开始，theme-next在写下这段文字时，版本为v7.8.0。由于默认情况下，实测V7版本在IOS浏览器中会出现主页空白的现象。这个现象需要将 motion 置 false 才可以消除。因此选择了V8以及以后的版本。

<!-- more -->

## fork主题并使用
由于在使用中会将主题进行修改，并希望保存配置，因此需要在gitHub页面将工程fork到自己的gitHub账户中。然后使用命令将Next主题仓库设置为站点source分支的子模块，放在 themes 目录下,：
```bash
git submodule add git@github.com:xiaorangood/hexo-theme-next.git themes/next
git commit -m "添加Next主题为子模块" && git push origin source
```
然后需改站点的 _config.yml 中主题设置：
``` yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
#theme: landscape
```
使用 hexo 命令重新生成网站并启动服务器，通过各终端查看效果
``` bash
hexo clean && hexo g && hexo s
```



## 设置主题样式
Next主题默认有4种样式，其中 Pisces 和 Gemini 暂时看不出区别，先选择了 Gemini 。打开主题的 _config.yml 文件，设置为：
``` yaml
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

## 设置页脚建站时间
Next主题在没有设置建站时间情况下，只会显示当前时间；在 themes/next/_config.yml 文件中搜索 since，设置起始时间为2018年。
``` yaml
footer:
  # Specify the year when the site was setup. If not defined, current year will be used.
  since: 2018
```

## 设置TOC目录的样式
在 themes/next/_config.yml 文件中搜索 toc；设置TOC目录不自动编码且不折叠：
``` yaml 
toc:
  enable: true
  # Automatically add list number to toc.
  number: false
  # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
  expand_all: true
```

## 设置站点主页和归档页面
在 themes/next/_config.yml 文件中搜索 menu；将 home 和 archives 前的注释去除。
``` yaml
menu:
  home: / || fa fa-home
  archives: /archives/ || fa fa-archive
```

## 页面显示当前浏览进度
在 themes/next/_config.yml 文件中搜索 scrollpercent；将false数值改为 true。
``` yaml
scrollpercent: true
```

## 设置代码块
在 themes/next/_config.yml 文件中搜索 copy_button，将复制按钮使能；查看 theme 下的 light 字段，将 light 字段的 default 修改为 monokai。
```yaml
codeblock:
  # Code Highlight theme
  # All available themes: https://theme-next.js.org/highlight/
  theme:
    # light: default
    # light: rainbow
    light: monokai
    # light: purebasic
    dark: stackoverflow-dark
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Available values: default | flat | mac
    style
```