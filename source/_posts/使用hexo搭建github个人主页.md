---
title: 使用hexo搭建github个人主页 -自用极简版
date: 2022-08-07 10:34:57
categories: 随记
tags: 
- hexo
- github
- 个人主页
---


## 安装nodeJs
可参考官方文档 [hexo-下载](https://nodejs.org/zh-cn/download/)

deepin 可能需要特殊处理

## 本地关联库
### github创建同名库
1. 使用github创建一个跟用户名同名的库，比如我的用户名是 breezehan，那么就创建一个 breezehan.github.io 的库
2. 根本地文件夹关联，或者先clone
   ``` bash
   $ git clone git@github.com:breezehan/breezehan.github.io.git my-blog
   ```

### hexo
``` bash
$ npm install hexo-cli -g
$ hexo init my-blog
$ cd my-blog
$ npm install
$ npm install hexo-deployer-git -save
$ git clone https://github.com/next-theme/hexo-theme-next themes/next
```
### 根目录的_config.yml
修改主题为：
theme: next

### 本地运行

``` bash
$ hexo g
$ hexo s
```
查看 http://localhost:4000/ 是否正常


### 部署到github
修改根目录 _config.yml
``` yml
deploy:
  type: git
  repo: git@github.com:breezehan/breezehan.github.io.git
  branch: master
```

``` bash
$ hexo g -d 
```
<!-- more --> 

## 保存源文件
### 在github上创建一个新分支，比如source，可以把主分支改为source

### 本地切换到source分支，修改 .gitignore ，只保留source目录和根目录下的文件

### submodules保存theme
``` bash
$ git submodule add https://github.com/next-theme/hexo-theme-next themes/next
```

### themes/next 的 _config.yml，可以在根目录中创建一个 _config.next.yml等方式保存


### push 到 github
``` bash
$ git add .
$ git commit-m "source分支保存源文件"
$ git push origin source
```

## 异地、异机使用

### 多级clone

``` bash
$ git clone --recurse-submodules git@github.com:breezehan/breezehan.github.io.git my-blog
```

### 环境配置
本地查看运行效果
``` bash
$ cd my-blog
$ npm install hexo
$ npm install hexo-deployer-git -save
$ hexo g
$ hexo s
```

## 标签、目录
### 打开配置:themes/next/_config.yml
``` yml
menu: 
  home: / || fa fa-home
  #about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```
### 新建tags page

``` bash
$ hexo new page tags
```
修改blog/source/tags/index.md，增加一行 type: "tags"
```
---
title: 标签
date: 2022-08-05 20:25:03
type: "tags"
---
```


### 新建categories page
``` bash
$ hexo new page categories
```

修改blog/source/categories/index.md，增加一行 type: "categories"

```
---
title: 文章分类
date: 2022-08-05 20:18:33
type: "categories"
---
```

### 文章中使用

``` bash
$ hexo new "xxxx"
```
文章中添加
```
---
title: 文章的标题
date: 发表时间，如：2021-08-15 08:15:16
description: 摘要(非必须)。也可以这一行删去，在文章中想要截断的地方加入<!--more-->，这样在首页就只显示开头到截断的内容，而不会显示全文
categories:
- 分类
- 子分类
tags:
- 标签1
- 标签2
---
```

## 其他
> 工具使用: vscode、typora

