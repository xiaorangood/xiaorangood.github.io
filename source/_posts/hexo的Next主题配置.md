---
title: hexo的Next主题配置
categories:
  - blog
tags:
  - 静态博客
  - hexo
  - Next主题
abbrlink: ff5f663b
date: 2022-03-26 23:52:03
---

# 选择仓库

在设置主题时候，无意间发现Next是有两个库，名字很相像，名字与地址分别是：

- [theme-next/hexo-theme-next](https://github.com/theme-next/hexo-theme-next)
- [next-theme/hexo-theme-next](https://github.com/next-theme/hexo-theme-next)

next-theme的主题，是从v8.0.0开始，theme-next在写下这段文字时，版本为v7.8.0。由于默认情况下，实测V7版本在IOS浏览器中会出现主页空白的现象。这个现象需要将 motion 置 false 才可以消除。因此选择了V8以及以后的版本。

主题配置可以参考[主题配置 - NexT 使用文档](https://theme-next.iissnan.com/theme-settings.html)。

<!-- more -->

# fork主题并使用

由于在使用中会将主题进行修改，并希望保存配置，因此需要在gitHub页面将工程fork到自己的gitHub账户中。然后使用命令将Next主题仓库设置为站点source分支的子模块，放在 themes 目录下,：

```bash
git submodule add git@github.com:xiaorangood/hexo-theme-next.git themes/next
git commit -m "添加Next主题为子模块" && git push origin source
```

然后需改站点的 _config.yml 中主题设置：

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
#theme: landscape
```

使用 hexo 命令重新生成网站并启动服务器，通过各终端查看效果

```bash
hexo clean && hexo g && hexo s
```

# 设置主题样式

Next主题默认有4种样式，其中 Pisces 和 Gemini 暂时看不出区别，先选择了 Gemini 。打开主题的 _config.yml 文件，设置为：

```yaml
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

# 设置页脚建站时间

Next主题在没有设置建站时间情况下，只会显示当前时间；在 themes/next/_config.yml 文件中搜索 since，设置起始时间为2018年。

```yaml
footer:
  # Specify the year when the site was setup. If not defined, current year will be used.
  since: 2018
```

# 设置TOC目录的样式

在 themes/next/_config.yml 文件中搜索 toc；设置TOC目录不自动编码且不折叠：

```yaml
toc:
  enable: true
  # Automatically add list number to toc.
  number: false
  # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
  expand_all: true
```

# 设置文章和TOC自动编号

## 通过hexo-heading-index插件的方法

参考[hexo-heading-index](https://github.com/r12f/hexo-heading-index)仓库。

步骤1：安装`hexo-heading-index`插件

```bash
npm install hexo-heading-index --save
```

步骤2：设置博客站点的配置文件`_config.yml`

```yaml
heading_index:
  enable: true
  index_styles: "{1} {1} {1} {1} {1} {1}"
  connector: "."
  global_prefix: ""
  global_suffix: " "
```

步骤3：在关闭主题配置文件`themes\next\_config.yml`的TOC目录自动编号功能

```yaml
toc:
  enable: true
  # Automatically add list number to toc.
  number: false
  # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
  expand_all: true
```

步骤4：执行命令重新生成博客网页

```bash
hexo clean && hexo g
```

## ccs方法

注意：该方法只能全局设置，且文章的编号必须从h1开始。

### 设置Next主题的CCS
打开文件`themes\next\source\css\main.styl `，在末尾添加如下代码：
``` ccs
.post-block {
  .post-body {counter-reset: h1}
          h1 {counter-reset: h2}
          h2 {counter-reset: h3}
          h3 {counter-reset: h4}
          h4 {counter-reset: h5}
          h5 {counter-reset: h6}
}
.post-body {
  h1:before {counter-increment: h1; content: counter(h1) ". "}
  h2:before {counter-increment: h2; content: counter(h1) "." counter(h2) ". "}
  h3:before {counter-increment: h3; content: counter(h1) "." counter(h2) "." counter(h3) ". "}
  h4:before {counter-increment: h4; content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) ". "}
  h5:before {counter-increment: h5; content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) ". "}
  h6:before {counter-increment: h6; content: counter(h1) "." counter(h2) "." counter(h3) "." counter(h4) "." counter(h5) "." counter(h6) ". "}
}
```

参考[Next Issues 873](https://github.com/theme-next/hexo-theme-next/issues/873#issuecomment-972586176)。

### 设置TOC目录自动编号
打开主题的配置文档`themes\next\_config.yml`,做如下配置：
```yaml
toc:
  enable: true
  # Automatically add list number to toc.
  number: true
```

# 设置站点主页和归档页面

在 themes/next/_config.yml 文件中搜索 menu；将 home 和 archives 前的注释去除。

```yaml
menu:
  home: / || fa fa-home
  archives: /archives/ || fa fa-archive
```

# 页面显示当前浏览进度

在 themes/next/_config.yml 文件中搜索 scrollpercent；将false数值改为 true。

```yaml
scrollpercent: true
```

# 设置代码块

在 主题配置（themes/next/_config.yml ）文件中搜索 copy_button，将复制按钮使能；查看 theme 下的 light 字段，将 light 字段的 default 修改为 monokai。

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

# 使能MathJax

 目前，NexT 提供两种数学公式渲染引擎，分别为 [MathJax](https://www.mathjax.org/) 和 [Katex](https://khan.github.io/KaTeX/)。本人选择了MathJax作为渲染引擎，主要考虑到该引擎相较更全面。

步骤1：Windows下载[Pandoc](https://github.com/jgm/pandoc/releases/tag/2.9.2.1)，并安装默认安装。

步骤2：卸载原有的渲染器 `hexo-renderer-marked`，并安装渲染器

```bash
npm uninstall hexo-renderer-marked
npm install hexo-renderer-pandoc
```

步骤3：设置Next主题的_config.yml文件(themes/next/_config.yml)

```yaml
math:
  every_page: true
  mathjax:
    enable: true
    # Available values: none | ams | all
    tags: none
    # See: https://mhchem.github.io/MathJax-mhchem/
    mhchem: false
  katex:
    enable: false
    # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
    copy_tex: false
```

参考文献：[Next主题的数学公式](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/MATH.md)

# 设置标签与分类

## 设置分类

步骤1：在终端窗口下，定位到 Hexo 站点目录下。使用 `hexo new page` 新建一个页面，命名为 `categories` ：

```bash
$ cd your-hexo-site
$ hexo new page categories
```

步骤2：编辑刚新建的页面，将页面的 `type` 设置为 `categories` ，主题将自动为这个页面显示分类。页面内容如下：

```markdown
title: 分类
date: 2022-05-03 13:53:41
type: "categories"
comments: false

---
```

步骤3：在菜单中添加链接。编辑 主题配置（themes/next/_config.yml）文件 ， 添加 `categories` 到 `menu` 中，如下:

```yaml
menu:
  home: /
  archives: /archives
  categories: /categoriesb
```

步骤4：在文章中分类标签

```markdown
categories:
- [父目录<,子目录><，子子目录>]
```

例如，下面为文章定义了三级目录，文章在`计算机/编程语言/C语言`这个目录下。

```
categories:
- [计算机,编程语言，C语言]
```

## 设置标签

步骤1：在终端窗口下，定位到 Hexo 站点目录下。使用 `hexo new page` 新建一个页面，命名为 `tags` ：

```bash
$ cd your-hexo-site
$ hexo new page categories
```

步骤2：编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：

```markdown
title: 分类
date: 2014-12-22 12:39:04
type: "categorie
comments: falses"
---
```

步骤3：在菜单中添加链接。编辑 主题配置文件 ， 添加 `tags` 到 `menu` 中，如下:

```yaml
menu:
  home: /
  archives: /archives
  tags: /tags
```

步骤4：在文章中使用标签Tags,例如

```markdown
tags: 
    - 静态博客
    - hexo
    - Next主题
```

## Hexo标签和分类的使用注意事项

[Front-matter | Hexo](https://hexo.io/zh-cn/docs/front-matter.html#%E5%88%86%E7%B1%BB%E5%92%8C%E6%A0%87%E7%AD%BE)

# 设置本地搜索

步骤1：安装插件

```bash
npm install hexo-generator-searchdb --save
```

步骤2：修改站点文件

```yaml
# Search 
search:
  path: ./public/search.xml
  field: post
  format: html
  limit: 10000
```

步骤3：修改主题配置文件

```yaml
# Local Search
# Dependencies: https://ithub.com/theme-next/hexo-generator-searchdb
local_search:
  enable: true
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 7
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false
```

# 设置Front-matter内容

新创建文章的时候，希望文件头带有标签等字符。

hexo具有的标记见[Front-matter | Hexo](https://hexo.io/zh-cn/docs/front-matter.html)。

只要设置`scaffolds/post.md`文件即可。

```mar
title: {{ title }}
date: {{ date }}
categories:
tags:
```

# 设置加载条

```yaml
pace:
  enable: true
  # All available colors:
  # black | blue | green | orange | pink | purple | red | silver | white | yellow
  color: blue
  # All available themes:
  # big-counter | bounce | barber-shop | center-atom | center-circle | center-radar | center-simple
  # corner-indicator | fill-left | flat-top | flash | loading-bar | mac-osx | material | minimal
  theme: minimal
```