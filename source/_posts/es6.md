---
title: es6 笔记
date: 2017-07-11 18:16:14
tag: ['es6']
categories: ['es6', '前端']
---

## let & const

声明变量

- 只在其代码块有效
- 不存在变量提升
- 暂时性死区

    * 暂时性死区：如果区块中存在let和const命令，这个区块对这些命令声明的变量从一开始就形成封闭的作用域
    ```
    var tmp = 123;

    if (true) {
        tmp = 'abc'; // ReferenceError
        let tmp;
    }
    ```
- 不允许重复声明

<!--more-->

> let

- 无

> const

- 声明常量，一旦声明，值不能改变
- 复合类型变量，变量名指向地址

## 变量的解构赋值

### 数组的解构

> [a, b] = [b, a]

### 对象的解构

> var { foo, bar } = { foo: 'aaa', bar: 'bbb' }

### 字符串的解构

> const [a, b, c, d, e] = 'bowen'

### 数值和布尔值的解构

> let {toString: s} = 123

### 函数参数的解构

```
function add([a, b]) {
    return a + b
}
```

## 字符串扩展

JavaScript内部，字符以UTF-16的格式存储，每个字符固定为2字节

### codePointAt()

### String.fromCodePoint()

### at()

### normalize()

### includes()，startsWith()，endsWith()

对应indexOf方法，接收第二个参数表示开始搜索的位置

- includes()

    返回布尔值，表示是否找到参数字符串

- startsWith()

    返回布尔值，表示参数字符串是否在源字符串头部

- endsWith()

    返回布尔值，表示参数字符串是否在源字符串尾部

### repeat()

参数是数字

- 小数会被取整
- 负数或Infinity会报错
- 0到-1之间的小数等同于0
- NaN等同于0
- 字符串先被转换为数字

### padStart()，padEnd()

字符串补全

- 第一个参数用来指定字符串最小长度
- 第二个参数用来补全，缺省则用空格补全

### 模板字符串

> \`i am ${name}\`

### String.raw()


## 正则的扩展

### RegExp 构造函数

### 字符串的正则方法

- match()
- replace()
- search()
- split()

### u修饰符

### y修饰符，sticky属性

sticky属性表示是否设置了y修饰符

### flags属性

返回正则表达式的修饰符

## 数值的扩展

## 数组的扩展

## 函数的扩展