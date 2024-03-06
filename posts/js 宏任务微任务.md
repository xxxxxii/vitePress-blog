---
author: yulinZ
pubDatetime: 2023-09-05
title: js 宏任务微任务
postSlug: js 宏任务微任务
featured: false
draft: false
tags:
  - 前端
  - js
  - 日常笔记
ogImage: ""
description: js 宏任务微任务
---

# js 宏任务微任务

js 由于是单线程执行，如果顺序执行任务就太慢了，前面的任务没执行完，后面的就需要等待，所以 js 就模拟了一种"多线程"机制同步任务和异步任务。

关于宏任务和微任务，异步任务分为宏任务和微任务

## js 任务执行机制

1. 先执行同步任务，在执行异步任务，异步任务中遇到宏任务，放入宏任务队列，微任务放入微任务队列

2. 异步遇到微任务，先执行微任务，执行完后如果没有微任务，就执行下一个宏任务，宏任务中如果有微任务，就按顺序一个一个执行微任务

   ![js-run](https://gitee.com/yulinzhu/pic-window/raw/master/js-run.png)

## 代码举例

```js
console.log("任务开始");
setTimeout(() => {
  console.log("延迟加载");
}, 100);

new Promise(resolve => {
  console.log("Promise");
  resolve();
}).then(() => {
  console.log("Promise then");
});

console.log("任务结束");
// 输出:
/*
任务开始
Promise
任务结束
Promise then
延迟加载
*/
```

分析：

​ console.log("任务开始");直接输出 任务开始

​ setTimeout(宏任务)放入队列

​ Promise->console.log("Promise");Promise 内部同步所以输出 Promise，遇到 Promise->then(微任务)放入队列

​ console.log("任务结束"); 直接输出 任务结束

所以同步执行完毕就输出了：任务开始 Promise 任务结束

下面执行异步（是否存在微任务）有一个执行 Promise->then 输出 Promise then，没有微任务执行宏任务，输出 延迟加载

上面是宏任务中没有微任务的去情况，下面看看宏任务中存在微任务

```js
console.log("任务开始");
setTimeout(() => {
  console.log("延迟加载");
  new Promise(resolve => {
    console.log("延迟加载 Promise");
    resolve();
  }).then(() => {
    console.log("延迟加载 Promise then");
  });
}, 100);

new Promise(resolve => {
  console.log("Promise");
  resolve();
}).then(() => {
  console.log("Promise then");
});

console.log("任务结束");
// 输出:
/*
任务开始
Promise
任务结束
Promise then
延迟加载
*/
```

分析：前面都不变 执行到 setTimeout 宏任务（宏任务中执行同步，同步，异步微任务），输出 延迟加载，然后执行 console.log("延迟加载 Promise");输出 延迟加载 Promise，再执行微任务 Promise().then 输出 延迟加载 Promise then

​
