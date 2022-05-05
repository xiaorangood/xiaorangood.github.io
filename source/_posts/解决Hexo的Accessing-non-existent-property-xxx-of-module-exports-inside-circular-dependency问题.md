---
title: >-
  解决Hexo的Accessing non-existent property 'xxx' of module exports inside circular
  dependency问题
abbrlink: afa63241
date: 2022-05-05 22:55:50
categories:
- blog
tags:
- hexo
- 静态博客
---

# 问题

运行`hexo s`后，出现下面所示的错误：

```bash
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
(node:15252) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(Use `node --trace-warnings ...` to show where the warning was created)
(node:15252) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:15252) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
(node:15252) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(node:15252) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:15252) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
```
<!--more-->
 
# 原因
通过搜索，直到了是因为`nib`使用了比较低版本的`stylus`。

参考链接：

[1]  https://www.haoyizebo.com/posts/710984d0/

[2]  https://gsgundam.com/2021-10-29-hexo-nodejs14-accessing-non-existent-property-issue/

# 解决方法

使用yarn指定包的版本。

步骤1：安装`yarn`
```bash
 npm install -g yarn
```

步骤2：修改博客站点的`package.json`文件
```
  "resolutions": {
    "stylus": "^0.54.8"
   }
```

步骤3：使用命令更新依赖包
```bash
 yarn install
```

经过依赖包跟新，则只能定了stylus使用的版本

