---
title: 在Windows下利用Hexo搭建个人博客
date: 2022-03-20 15:26:46
tags: 
---

## 本地创建个人博客
### 安装 git 工具

从[git官网](https://git-scm.com/downloads)下载windows下的软件，本文按照时的软件版本为 2.35.1。

安装软件时，使用默认设置一直点击 Next 按钮，一直到下图的页面勾选两个选项；然后点击 Install 安装 git 软件。
![](https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_16-10-29.png)

勾选“Enable experimental support for pseudo consoles”选项是为了在 git bash 中启动 Hexo 服务后，可以通过 Ctrl + c 停止 Hexo 服务器的运行。

### 安装node.js
Hexo是基于Node.js的，因此在安装Hexo前，需要安装该软件。

从 [Node.js官网](https://nodejs.org/zh-cn/)下载软件，当前版本号是 17.7.2。

下载软件后，按照默认设置安装即可。

### 安装 Hexo 软件
执行以下几个命令安装
```shell
# 将npm镜像修改为淘宝镜像
$ npm config set registry "https://registry.npm.taobao.org"
# 使用npm安装 Hexo
$ npm install -g hexo-cli
# 在当前目录下初始化一个博客目录，并进入该目录
$ hexo init blog
$ cd blog
# 在博客目录使用命令启动Hexo服务器
$ hexo s
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```
浏览器后，输入`http://localhost:4000/`即可打开博客网页。
如果希望在其他端口打开网页，可以使用 Hexo 命令指定端口。例如指定端口为5000。
```shell
$ hexo s -p 5000
```

### 创建Hexo文件
执行以下命令后，Hexo会在`source\_posts`目录下创建以文章名命名的markdown文件
```shell
$ hexo n "文章名"
```
然后执行命令生成html文件
```shell
$ hexo g
```
最后使用命令运行 Hexo 服务器即可看到新内容



## 部署博客到Git Pages
### 创建博客仓库
在github页面中，创建新仓库，仓库名字为`xiaorangood.github.io`。

### 安装自动部署工具并设置
执行以下命令安装部署工具：
```shell
$ npm install --save hexo-deployer-git
```
设置`_config.yml`文件内容：
```
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: git@github.com:xiaorangood/xiaorangood.github.io.git
  branch: master
```
### 测试网络连接
通过命令生成 ssh 密钥:
```shell
$ ssh-keygen
$ cat ~/.ssh/id_rsa.pub
```
在获得密钥后，添加到github的个人设置页面中添加密钥：
![](https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_17-38-44.png)
添加密钥后，通过命令验证是否连接成功：
```shell
$ ssh -T git@github.com
Hi xiaorangood! You've successfully authenticated, but GitHub does not provide shell access.
```
如果出现超时的现象，通过命令设置 git 的代理：
```shell
git config --global http.proxy 'socks5://127.0.0.1:10809'
git config --global https.proxy 'socks5://127.0.0.1:10809'
```
### 部署个人博客网页
在blog的目录下执行命令部署个人博客：
```shell
$ hexo clean
$ hexo g
$ hexo d
```

## 使用source分支来保存博客源文件
### 在 github 上创建新分支
上个章节中展示了使用 master 分支来保存生成的博客页面的方法，但原来的markdown文件并没有保存。为了保存 Markdown 文件，在仓库中创建`source`分支。

![](https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_17-58-33.png)

将source分支修改为默认分支：

![](https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_18-06-26.png)

检查仓库的默认分支：

![](https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/Snipaste_2022-03-20_18-07-14.png)

### 设置本地仓库
在 blog 所在目录，执行仓库初始化，并设置远端仓库的地址。然后切换到目标分支。这里我的博客是在`D:/blog/`目录下。
```shell
$ git init
Initialized empty Git repository in D:/blog/.git/
$ git remote add origin git@github.com:xiaorangood/xiaorangood.github.io.git
$ git checkout source --
```
因为我们只需要保留博客源码，其他无关的文件并不希望推送，需要确保配好了.gitignore文件，通常如下：
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
_multiconfig.yml
```

### 提交源文件
```shell
$ git add .
$ git commit -m 'Regular save'
$ git push origin source
```

### 删除非源文件
由于source分支是从master复制而来，所以有一些是deployment文件。这些部署的文件可以删除，也可以理会。
删除文件夹后只剩下如下的文件夹。
```shell
node_modules/  scaffolds/  source/  themes/
```