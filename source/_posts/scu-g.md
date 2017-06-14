---
title: 毕业设计
date: 2016-6-1
tags: ['express', 'node', 'mysql']
categories: ['scu']
---

## 毕业设计

收拾整理为知笔记，这里将毕业设计的部分笔记写成博客后移除为知笔记。

<!--more-->

### 关于毕业设计

毕业设计我做的是基于数据分析的高考志愿填报系统。

Q:为何基于数据分析？

A:因为只有十年间的高考数据可以和仅能作为参考。算不上数据挖掘。

Q:使用到的技术？

A:我是前端开发工程师。技术栈前端使用<code>angularjs1</code> 框架，后台接口使用 <code>express</code> 框架，数据库 <code>mysql</code> 。系统最主要的模型是斗斗学姐通过多元线性回归做的，我只需要将模型转换为code就可以了。

### 笔记

#### 爬虫

* <code>request</code>

    > request(url, function (error, response, body) {}

* <code>cheerio</code>

    > var $ = cheerio.load(body.data);

#### express

* 新建 <code>express</code>

    > express app

* 配置端口

    ```
    app.set('port', process.env.PORT || 3000);
    app.listen(app.get('port'), function () {
        console.log('Express server listening on port ' + app.get('port'));
    });
    ```

* 设置模板引擎

    ```
    var ejs = require('ejs');
    app.set('views', __dirname + '/views');
    app.engine('.html', ejs.__express);
    app.set('view engine', 'html');
    ```

* 使用静态文件

    > app.use(express.static('app'));

#### mysql

* 配置 <code>mysql</code>

    ```
    var _mysql = require('mysql');
    var HOST = 'localhost',
        PORT = '3306',
        MYSQL_USER = 'root',
        MYSQL_PASS = '123456',
        DATABASE = 'scu',
        CHARSET = 'UTF8';

    var config = {
        host: HOST,
        port: PORT,
        user: MYSQL_USER,
        password: MYSQL_PASS,
        charset: CHARSET
    };
    ```

* 连接 <code>mysql</code> 回调

    ```
    var Connect = function(sql, sql_params) {

        var mysql = _mysql.createConnection(config);
        mysql.query('use ' + DATABASE, function(error, results) {
            if(error) {
                console.log('ClientConnectionReady Error: ' + error.message);
                mysql.end();
                return;
            }
        });

        mysql.query(sql,sql_params,function (err, result) {
            if(err){
                console.log('ERROR] - ',err.message);
                return;
            }
        });

        mysql.end();
    };
    ```