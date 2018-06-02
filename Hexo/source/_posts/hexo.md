---
title: Hexo 搭建自己的博客
date: 2017-04-19 20:45:14
categories: "Hexo" #哪个分类下
tags: [Hexo]
description:  #描述
---

# Hexo
Hexo是一个开源的静态博客生成器,用node.js开发。

# 搭建博客的初衷
每当自己(学习、coding)中，总会遇见问题，就Baidu、Google 看别人的讨论或者博客。其实写博客或者发表一个详细的技术点的时候，就是对于自己的沉淀和巩固。这是我所欠缺的，很多东西我都是需要实践来取证自己所知道知识。所以闲暇之余，我要养成写博客的习惯。`(其实我是怕 说的技术点不够准确，或者有误区 希望大家来指正)`

<!--more-->

------

#### 注:习惯用Mac  所以`Shell`命令行开头：`$ ` 替换盘符：`D:...Blog\Hexo`

[TOC]


# 一、准本工作：
## 1、检查
是否安装了Node.js

```shell
$ node -v

#如果有版本号，说明你已经安装过了 (例如我的:`v6.10.2`)
#Node更新等等操作，我想你会的。
```

## 2、安装软件
   > 安装软件:(我个人在家用的是Win10)
   - [github.desktop](https://desktop.github.com/)： 安装这个会自动安装`Git Shell`这样我们就不用安装git了
   - [node.js](https://nodejs.org/en/download/):  Hexo是一款基于Node.js的静态博客框架，所以先安装Node.js。



# 安装Hexo
## 1、新建 `Blog` 文件夹，我是放到了 `D:` ,根据个人情况。
```shell
D:\softwork\Blog\
```

## 2、用淘宝镜像 安装Hexo
```shell
#进入到相应的盘符和目标文件夹
$ npm install -g hexo --registry=https://registry.npm.taobao.org

注:我家里的网不好，翻墙后的网速也不可观，如果你的网络好的话，使用下面的:
$ npm install hexo-cli -g
```

## 3、检测 `Hexo` 是否安装上
```shell
$ hexo

#会出现一些命令说明的东西，那么你的Hexo就安装成功了
```

## 4、Hexo 初始化
```shell
$ hexo init <folder>

#例如:
$ hexo init Hexo
```

## 5、可以浏览本地服务器生成的静态HTML
```shell
$ cd .\Hexo\

#安装NPM(NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题)
$ npm install

# 生成静态页面
$ hexo generate 或者 hexo g

# 启动本地服务
$ hexo serve 或者 hexo s
```

## 6、在GitHub上新建一个 `new repository(新的存储库)` (默认300M 这个应该够用了)
注: Owner 一定是自己的账户名，不是`organization(组织)`名
看了好多文章都说`Repository name` 都是xxx.`github.io`，这个`github.io`都是这么写。不这么写会有什么错误。我想说不会，但是我看过有不是以这个结尾的，如果你是新手，还是这么写吧！
![github_repository](/uploads/github_repository.png)

## 7、进入刚刚新建的 `new repository` 右边有个 `Setting`
(1)配置 GitHub Pages (用于介绍托管在GitHub的项目)
(2)Choose a theme
![Pages_choseTheme](/uploads/Pages_choseTheme.jpg)

你部署完服务器，可以马上浏览的页面

GitHub上的工作就做完了，回到本地

## 8、用Notepad++配置 `站点配置文件`
因为`Win10记事本`编写的中文生成的静态页不是标准的UTF-8，会导致乱码 ，所以用Notepad++ 编写。
![Notepad_utf8](/uploads/Notepad_utf8.jpg)

设置 Notepad++ 自动换行功能 和 行宽
![Nodepad_auroNewline_lineWidth](/uploads/Nodepad_auroNewline_lineWidth.jpg)

下面编写 `站点配置文件`
```shell
# Site
#网站的标题
title: srxboys
#副标题
subtitle: 说点什么好呢？
#描述
description: 22joke
 #作者信息
author: srxboys
#头像，图片位置在相应主题目录下的images
#avatar: /images/avatar.png
language: zh-Hans

deploy:
#部署环境，基于hexo+githubpage,所以这里使用git。注意：不同版本的hexo，type有可能不同，3.x以后应使用git,具体参看官方文档
   type: git
#git仓库地址，替换成你的username即可，其他保持不变，后面会提到如何创建git仓库
   repository: git@github.com:srxboys/srxboys.github.io.git

   branch: master

```

repository : 的内容最好不要手动，GitHub有 copy 的SSH地址
![copy_github_userSSH](/uploads/copy_github_userSSH.jpg)

最近发现[ Atom ](www.atom.io)编写Mackdown,是比较不错的，还可以边写边看效果。
```sh
# 推荐插件
Mackdown-preview
```

## 9、生成的静态页署到GitHub上
```shell
$ hexo clean

# 生成静态页面
$ hexo generate

# 部署远程网站
$ hexo deploy
```

## 10、hexo deploy 部署远程网站 `错误`
```shell
$ hexo deploy
ERROR Deployer not found:

#补救方法：
$ npm install hexo-deployer-git --save
```

----

# 其他注意事项:
配置信息文件
属性：`空格` <相应的值>    ---> 这里要一定注意 `冒号`后面要有个 `空格`,避免在 `generate` 时出错

over !   over !   over !
