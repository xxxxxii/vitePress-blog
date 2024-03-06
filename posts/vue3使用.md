---
author: yulinZ
pubDatetime: 2023-09-05
title: vue3 基础使用
postSlug: vue3 基础使用
featured: false
draft: false
tags:
  - 前端
  - js
  - 日常笔记
ogImage: ""
description: vue3 基础使用
---

**vue3 使用**

# 创建项目

` npm init vite 项目名称`

# 使用 router

`npm install vue-router@4`

## 使用

创建 router/index.ts

```typescript
import { createRouter, createWebHashHistory } from "vue-router";

// 1. 定义路由组件
const Main = {
  render() {
    return "vue3-vite 基础模板:已配置路由，pinia";
  },
};

// 2. 定义一些路由：每个路由都需要映射到一个组件。
const routes = [
  {
    path: "/",
    component: Main,
  },
  {
    path: "/home",
    // 路由懒加载
    component: () => import("../pages/home/index.vue"),
  },
];

// 3. 创建路由实例并传递 `routes` 配置。
const router = createRouter({
  // 内部提供了 history 模式的实现。为了简单起见，我们在这里使用 hash 模式。
  history: createWebHashHistory(),
  routes, // `routes: routes` 的缩写
});

export default router;
```

mian.ts 中导入

```typescript
import { createApp } from "vue";
import "./style/style.css";
import App from "./App.vue";
import router from "./router";

async function bootstrap() {
  const app = createApp(App);

  app.use(router);
  app.mount("#app");
}

void bootstrap();
```

App.vue 添加` <router-view />`

# 使用 axios

`npm install axios --save`

## 使用

创建 http 文件夹

# pinia

`pnpm install pinia  `

pinia 持久化插件

`npm i pinia-plugin-persist --save`

## 使用

持久化

enabled: true 即表示开启数据缓存

```js
// 开启数据缓存
persist: {
  enabled: true;
}
```

这个时候数据默认是存在 sessionStorage 里，需要修改的话如下

```js
persist: {
  enabled: true,
  strategies: [
    {
      key: 'userInfo',//设置存储的key
      storage: localStorage,//表示存储在localStorage
    }
  ]
}
```

默认所有 state 都会进行缓存,如果你不想所有的数据都持久化存储，那么可以通过 paths 指定要长久化的字段，其余的字段则不会进行长久化，如下:

```js
persist: {
  enabled: true,
  strategies: [
    {
      storage: localStorage,
      paths: ['id'],//指定要长久化的字段
    }
  ]
}
```

# scss

`npm i sass node-sass sass-loader -s`
