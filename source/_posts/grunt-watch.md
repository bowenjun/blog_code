---
title: grunt
date: 2017-05-26 21:16:14
tag: ['grunt']
categories: ['webpack-grunt-glup']
---

### 配置

<!--more-->

```
module.exports = function(grunt) {

    // 配置
    grunt.initConfig({
        pkg : grunt.file.readJSON('package.json'),
        uglify : {
            options : {
                banner : '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd HH:MM:ss") %> */\n'
            },
            build : {
                options: {
                    mangle: false
                },
                files: {
                    'build/app.min.js': [
                        'app/*.js', 'app/*/*.js', 'app/*/*/*.js', 'app/*/*/*/*.js'
                    ]
                }
            }
        },
        less: {
            compile: {
                options: {
                    paths: ["app/app/css"]
                },
                files: {
                    "build/style.css": "app/css/main.less"
                }
            }
        },
        watch: {
            scripts: {
                files: ['app/css/*.less', 'app/*.js', 'app/*/*.js', 'app/*/*/*.js', 'app/*/*/*/*.js'],
                tasks: ['less', 'uglify']
            }
        }
    });

    // 载入uglify插件
    grunt.loadNpmTasks('grunt-contrib-uglify');

    // less
    grunt.loadNpmTasks('grunt-contrib-less');

    // watch
    grunt.loadNpmTasks('grunt-contrib-watch');

    // 注册任务
    grunt.registerTask('default', ['uglify', 'less', 'watch']);
};
```

### 配置说明

* <code>initConfig uglify</code>

    <code>build</code> 通过 <code>*</code> 通配文件，并将js压缩，结果存放到 <code>build/app.min.js</code>

* <code>initConfig less</code>

    <code>compile</code> 直接将  <code>main.less</code> 文件通过 <code>grunt-contrib-less</code> 转换为 <code>css</code>，在 <code>main.less</code> 中通过 <code>import</code> 导入的文件也会被转换，最终生成一个 <code>css</code> 文件为 <code>build/app.min.js</code>

* <code>initConfig watch</code>

    <code>scripts watch</code> 通过  <code>*</code> 通配变化的文件，若文件内容发生变化，会执行 <code>uglify</code> 和 <code>less</code> 这两个 <code>tasks</code>

* 插件

    * <code>grunt.loadNpmTasks('grunt-contrib-uglify');</code>
    * <code>grunt.loadNpmTasks('grunt-contrib-less');</code>
    * <code>grunt.loadNpmTasks('grunt-contrib-watch');</code>
    
* 注册

    配置完成之后执行注册任务

    > <code>grunt.registerTask('default', ['uglify', 'less', 'watch']);</code>


### package.json

```
{
  "name": "grunt",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.0",
    "grunt-contrib-concat": "~0.2.0",
    "grunt-contrib-jshint": "~0.6.5",
    "grunt-contrib-less": "^1.4.0",
    "grunt-contrib-uglify": "~0.2.7",
    "grunt-contrib-watch": "^1.0.0",
    "grunt-jsdoc": "^2.1.0"
  }
}
```

### 常见问题

Q: <code>grunt: watch ENOSPC</code>

A: <code>echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p</code>