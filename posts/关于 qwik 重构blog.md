---
author: yulinZ
date: 2023-09-05
title: qwik 重构 blog
postSlug: qwik 重构 blog
featured: true
draft: false
tags:
  - 前端
  - qwik
  - 日常笔记
ogImage: ""
description: qwik 重构 blog
---

<!--T qwik 重构 blog -->

<!--@为优化 seo 而重构 blog 网站,性能分析@-->

<!--@class 前端 @-->

<!--@keys 前端,性能,重构,web @-->

<!--@!!@-->

# 关于 qwik 重构 blog

## 1. 对比之前的网站

采用的是 nuxt.js,网站的整体得分并不理想。

![](https://gitee.com/yulinzhu/pic-window/raw/master//f8a9fc79d20869e92d5e7f58a225395f.png)
下面是使用 qwik 重构的
![](https://gitee.com/yulinzhu/pic-window/raw/master//0b532916bd197404cad58fa09fcab4de.png)

虽然重构的项目其实是采用的极简设计，页面上基本没使用图片，或许这也是重构版可以获得较高分的原因之一，但是对于 seo 的设置和之前基本保持一致。qwik 不需要怎么去设置就能够达到很不错的效果。这或许也是目前 qwik 火的原因之一。

## 对 qwik 看法

qwik 这个框架其实出来已经 2 年了，也是最近不知道为什么这么火，这里我只谈谈开发项目中使用 qwik 的感受。

1. qwik 在 seo 这一方面确实不错，页面的整体加载速度，性能等等。
2. 能够兼容 react 组件 api 等等，具体应该是转译的方式，官方文档有教程，我并没有用到。
3. 开发方式和 react 类似，但并不是一个东西，也是采用 jsx 来编译模版。
4. 文档全英文，官方的例子也是很简单的，项目中遇到问题能够支持的解决方案可以说很少。还有就是生态并不完善。想 ui 这些基本上都要自己完全手撸。
5. 网上相关的资料基本上没有。

# 虽然目前 qwik 有缺点但有很大的潜力

1. 以 html 优先的概念，使得用户体验较好，这也是 seo 项目重要的指标之一。
2. 非常巧妙的可以说是无 hydration(水合) 的过程，省略了传统 SSR 下首屏需要加载庞大的 JS，惰性加载事件。这就是 qwik 快的原因。
