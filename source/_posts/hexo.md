---
title: hexo 简易教程
date: 2017-03-26 21:16:14
tag: ["hexo"]
---

### hexo 使用教程
- - - - 
详见：[hexo官方教程](https://hexo.io/zh-cn)
- - - -

#### 安装
```
$ npm install -g hexo-cli
```
<!--more-->

#### 建站
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

#### 常用指令
> new 

```
$ hexo new [layout] <title>
```
新建一篇文章

> generate

```
$ hexo generate
$ hexo g (简写)
```
生成静态文件

> server

```
$ hexo server
```
启动服务器(默认4000端口)

> deploy

```
$ hexo deploy
$ hexo d (简写)
$ hexo d -g (部署之前预先生成静态文件)
```
部署网站

> clean

```
$ hexo clean
```
清除缓存文件和已生成的静态文件