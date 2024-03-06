---
author: yulinZ
pubDatetime: 2023-09-05
title: ES6 var let const 区别
postSlug: ES6 var let const 区别
featured: false
draft: false
tags:
  - 前端
  - ES6
  - 日常笔记
ogImage: ""
description: ES6 var let const 区别
---

# ES6 var let const 区别

ES6 新增加了 let const 2 个声明关键字，推荐使用 let const，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。这样的错误在 ES5 是很常见的，现在有了这种规定，避免此类错误就很容易了。下面就详细了解一下

## var

1. 变量提升(声明提升)

   ```js
   console.log(num); // undefined
   var num = "123";
   ```

2. 变量覆盖

   ```js
   var num = "12"；
   var num = "23"；
   console.log(num); // 23
   ```

3. 没有块级作用域

   ```js
   functtion fn() {
       for(var i = 0; i < 3; i++){
           console.log(i); // 0 1 2
       }
       console.log(i); // 3
   }
   ```

# let

把上面 var 换成 let 会报错，更容易发现错误，代码也更加严谨。

1. 只在块作用域有效
2. 没有变量提升，存在暂时性死区
3. 不能重复声明

# const

1. 声明后必须赋值，否则报错
2. 定义的值不能修改
3. 支持 let 的属性
