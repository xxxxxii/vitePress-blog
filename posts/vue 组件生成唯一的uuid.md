---
author: yulinZ
pubDatetime: 2023-09-05
title: 为组件生成唯一的id
postSlug: 为组件生成唯一的id
featured: false
draft: false
tags:
  - 前端
  - 日常笔记
ogImage: ""
description: 为组件生成唯一的id,uuid
---

# vue 组件生成唯一的 uuid

今天在开发组件时因为使用`<input id="id" type="checkbox" />`和` <label for="id">` 绑定 id，组件复用时 id 不唯一产生的 bug，如下图：

![image-20230328151117111](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230328151117111.png)

# 问题分析

点击后面 switch 按钮时都只会影响到第一个，这个问题肯定是 id 问题，所以每次实例化组件时都需要为组件生成唯一的 id，下面就看如何生成一个唯一的 id，这边使用 uuid，uuid 在后端可以说使用得很多。UUID 只是一个值，您可以放心地将其视为唯一值。碰撞的风险是如此之低，以至于您可以合理地选择完全忽略它。您可能会看到 UUID 使用不同的术语（[GUID](https://so.csdn.net/so/search?q=GUID&spm=1001.2101.3001.7020) 或 Globally Unique Identifier，是 Microsoft 的首选语义）来引用，但含义和效果保持不变。 大家如果不了解可以去了解一下。

# 实现

```typescript
function uuidv4() {
  //1e7]+-1e3+-4e3+-8e3+-1e11 = 10000000-1000-4000-8000-100000000000,我这边使用的ts 用1e7]+-1e3+-4e3+-8e3+-1e11会报红线所以直接使用计算后的结果
  return "10000000-1000-4000-8000-100000000000".replace(/[018]/g, (c: any) =>
    (
      c ^
      (crypto.getRandomValues(new Uint8Array(1))[0] & (15 >> (c / 4)))
    ).toString(16)
  );
}
```

# 结果

![image-20230328152611824](C:\Users\Windows12.2Pro\Desktop\image-20230328152611824.png)

可以看到问题已经完美解决，所以说在开发中如果组件复用涉及到 id 的绑定且不确定的时候，可以往这方面想一想。
