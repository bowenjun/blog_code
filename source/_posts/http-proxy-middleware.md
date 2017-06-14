---
title: http-proxy-middleware代理前端系统
date: 2017-5-4
tags: ['proxy', 'express', 'node', 'javascript']
---

#### 安装

> npm install --save-dev http-proxy-middleware

<!--more-->

#### 配置

使用 express 搭建服务器

```
...

var proxyTable = require('./proxy/proxy');
var proxy = require('http-proxy-middleware');
...

// proxy api requests
// 顺序必须在 bodyParser 之前！！！
Object.keys(proxyTable).forEach(function(context) {
  var options = proxyTable[context]
  if (typeof options === 'string') {
    options = {
      target: options
    }
  }
  app.use(proxy(options.filter || context, options));
})
```
proxy/proxy.js 配置

```
// 这里只提供基本用法 , 更多配置请参考 http-proxy-middleware readme
module.exports = {
  '/api': {
    target: 'http://yourUrl:port1/',
    changeOrigin: true,
    pathRewrite: {
      '^/api': ''
    }
  },
  '/auth': {
    target: 'http://yourUrl:port2/',
    changeOrigin: true,
    pathRewrite: {
      '^/auth': '/auth'
    },
    onProxyReq: function(proxyReq, req, res) {
      proxyReq.setHeader('add', 'xx')
    }
  }
}
```

#### 工具手架

如果你是想要直接将前端代码跑起来，node-1742 是我提供了一个可以使用 npm 获取并开箱即用的包。


```
// 1. 下载
npm install -g node-1742

// 2. 命令生成
// * new folder
node-1742 init new-folder
cd new-folder

// * exist folder
cd exist-folder
node-1742 init

// 3. 安装依赖
npm install

// 4. 在 proxy/proxy.js 中配置代理

// 5. 将前端文件放入 public 文件夹中，入口为 public/index.html

// 6. 运行
npm start
```

#### Q & A

> 通过 ajax 发送的请求后台接收不到 data ？

错误原因：

app.use(bodyParser.json());

app.use(bodyParser.urlencoded({ extended: false }));

将数据做了处理。

解决办法：

将 proxy 的 order 提到 bodyParser 之前

#### 参考

github : [http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware)

vue-cli : config/index.js proxyTable && build/dev-server.js

