---
title: Next主题自定义友情链接
date: 2022-05-03 14:52:31
categories:
- blog
tags: 
- 静态博客
- hexo
- Next主题
---

Next主题版本：8.10.1

# 新增 links 页面

在控制台使用命令创建：

```bash
hexo new page links
```

也可在博客根目录 /source 下手动创建 links 文件夹和里边的 index.md 文件。

# 编辑links对应的文档

在博客根目录 /source 下会生成一个 links 文件夹，打开其中的 index.md 文件，做如下编辑：

```markdown
title: 友情链接
date: 2022-05-03 14:34:43
type: "links"
```

# 编辑主题配置文件

在主题配置（themes/next/_config.yml)文件中，menu目录下添加如下配置：

```yaml
menu:
  links: /links/ || fas fa-link
```

在 `/themes/next/languages/zh-CN.yml` 文件中 `menu` 下增加中文描述

```yaml
menu:
  links: 友链
```

# 设置友链页面样式

在`themes\next\layout\_partials\page`里新建`links.njk`文件，添加如下代码：

```js
{% block content %}
  {######################}
  {### LINKS BLOCK ###}
  {######################}
    <div id="links">
        <style>
            .links-content{
                margin-top:1rem;
            }

            .link-navigation::after {
                content: " ";
                display: block;
                clear: both;
            }

            .card {
                width: 300px;
                font-size: 1rem;
                padding: 10px 20px;
                border-radius: 4px;
                transition-duration: 0.15s;
                margin-bottom: 1rem;
                display:flex;
            }
            .card:nth-child(odd) {
                float: left;
            }
            .card:nth-child(even) {
                float: left;
            }
            .card:hover {
                transform: scale(1.1);
                box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.12), 0 0 6px 0 rgba(0, 0, 0, 0.04);
            }
            .card a {
                border:none; 
            }
            .card .ava {
                width: 3rem!important;
                height: 3rem!important;
                margin:0!important;
                margin-right: 1em!important;
                border-radius:4px;

            }
            .card .card-header {
                font-style: italic;
                overflow: hidden;
                width: 236px;
            }
            .card .card-header a {
                font-style: normal;
                color: #2bbc8a;
                font-weight: bold;
                text-decoration: none;
            }
            .card .card-header a:hover {
                color: #d480aa;
                text-decoration: none;
            }
            .card .card-header .info {
                font-style:normal;
                color:#a3a3a3;
                font-size:14px;
                min-width: 0;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
            }
        </style>
        <div class="links-content">
            <div class="link-navigation">
                {% for link in theme.mylinks %}
                    <div class="card">
                        <img class="ava" src="{{ link.avatar }}"/>
                        <div class="card-header">
                        <div><a href="{{ link.site }}" target="_blank">@ {{ link.nickname }}</a></div>
                        <div class="info">{{ link.info }}</div>
                        </div>
                    </div>
                {% endfor %}
            </div>
            {{ page.content }}
            </div>
        </div>
  {##########################}
  {### END LINKS BLOCK ###}
  {##########################}
{% endblock %}}
```

修改`themes/next/layout/page.njk`文件，**注意格式**。 在

```js
{%- elif page.type === 'schedule' and not page.title %}
    {{- __('title.schedule') + page_title_suffix }}
```

下面添加：

```js
{%- elif page.type === 'links' and not page.title %}
  {{- __('title.links') + page_title_suffix }}
```

在

```js
{% elif page.type === 'schedule' %}
  {%- include '_partials/page/schedule.njk' -%}
```

下面添加：

```js
{% elif page.type === 'links' %}
  {%- include '_partials/page/links.njk' -%}
```

# 设置友情链接页面

在主题配置（themes/next/_config.yml)文件末尾处添加友链：

```yaml
mylinks:
  - nickname:  #友链名称
    avatar:   #友链头像
    site:   #友链地址
    info:   #友链说明
  - nickname:  #友链名称
    avatar:   #友链头像
    site:   #友链地址
    info:   #友链说明
```
