---
author: yulinZ
pubDatetime: 2023-09-05
title: vue3 + vite npm 组件库开发(一)
postSlug: vue3 + vite npm 组件库开发(一)
featured: true
draft: false
tags:
  - 前端
  - vue
  - 日常笔记
ogImage: ""
description: vue3 + vite npm 组件库开发(一)
---

# vue3 + vite npm 组件库开发(一)

简述 vue3 vite 开发组件库并上传 npm 过程第一章

# 1.创建项目

创建一个普通的 vite vue3 项目即可，我这里创建的是 ts 的项目，js 也可，根据自己的使用习惯。

# 2.配置项目

1. 根目录下创建 packages 目录作为组件的开发包,目录下 index.ts 作为整个组件库的出口文件，导出组件

   index.ts

   ```typescript
   import zButton from "./button/index";

   import { App } from "vue";

   const install = (app: App) => {
     app.use(zButton);
   };
   const ZUI = {
     install,
   };
   // 这是为了按需加载
   export { zButton, zInput, zTextarea };
   // 这里可以直接使用组件库
   export default ZUI;
   ```

2. packages 中创建一个组件目录，目录中至少有 index.ts 出口文件 和 组件模板文件：例如 button.vue

   button.vue 就是常规的组件封装

   index.ts

   ```typescript
   import zButton from "./button.vue";
   import { App } from "vue";

   zButton.install = (app: App) => {
     app.component(zButton.name, zButton);
   };

   export default zButton;
   ```

3. vite.config 中配置打包

   ```typescript
   import { defineConfig } from "vite";
   import vue from "@vitejs/plugin-vue";

   // https://vitejs.dev/config/
   export default defineConfig({
     plugins: [vue()],

     build: {
       // 这里配置打包，打包时要排除Vue的依赖，因为我们使用组件库时本地肯定是vue 环境，否则会报isCE 的错误
       rollupOptions: {
         external: ["vue"],
         output: {
           globals: {
             vue: "Vue",
           },
         },
       },
       // 设置打包的文件和名称，名称这里可以先去npm官网搜索一下是否存在，否则后面发包不成功也要修改
       lib: {
         entry: "./packages/index.ts",
         name: "v3-zy-ui",
       },
     },
   });
   ```

   下面执行 npm run build 命令会在 dist 文件夹下生成这样几个文件，如果是 js 项目，没有 mjs 的文件而是包含 es 的文件，这个没有影响

   ![image-20230302150107674](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302150107674.png)

4. 配置 package.json

   ```json
   {
     "name": "v3-zy-ui",
     "private": false,
     "version": "0.0.3",
     "description": "",
     "main": "./dist/v3-zy-ui.umd.js",
     "module": "./dist/v3-zy-ui.mjs",
     "exports": {
       ".": {
         "import": "./dist/v3-zy-ui.mjs",
         "require": "./dist/v3-zy-ui.umd.js"
       }
     },
     "files": ["dist/*"],
     // 主要是前面的配置，js项目就把mjs相关的替换成打包出来的另一个即可
     "scripts": {
       "dev": "vite --mode dev",
       "build": "vite build --mode prod",
       "preview": "vite preview --mode prod"
     },
     "dependencies": {
       "md-editor-v3": "^2.8.1",
       "v3-zy-ui": "^0.0.3",
       "vue": "^3.2.45",
       "vue-router": "^4.1.6"
     },
     "devDependencies": {
       "@icon-park/vue-next": "^1.4.2",
       "@types/node": "^18.14.2",
       "@vitejs/plugin-vue": "^4.0.0",
       "typescript": "^4.9.3",
       "vite": "^4.1.4",
       "vite-plugin-vue-markdown": "^0.22.4",
       "vue-tsc": "^1.0.24"
     }
   }
   ```

   配置好了就 npm run build 测试一下是否打包成功

# 3. 组件库上传 npm

## 首先你得有 npm 账号

首先要在 npm 官网注册自己的 npm 账户，链接：https://www.npmjs.com/

## 查询是否存在包名

前面查了的就不用查了，可以 npm 官网上查也可 `npm view  包名`

没有查到或者执行命令出现下图即不存在包，可以使用该名称

![image-20230302151357421](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302151357421.png)

## 上传包必须使用 npm 官方源如果配置了淘宝镜像需要修改回来

（1）查看当前源：npm config get registry

（2）切换为 npm 源：npm config set registry https://registry.npmjs.org

（3）切换为淘宝镜像：npm config set registry=https://registry.npm.taobao.org/

## 添加自己的账户

`npm login` 点击出现的链接跟着做就行了，会验证邮箱这些

![image-20230302151815895](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302151815895.png)

登录完了可通过 `npm who am i`查看是否登录成功，出现自己的账户名即成功

## 上传包

`npm publish` 没有报错就上传成功了，报错请自行查找问题

npm 登录就可以查看到自己的包了

![image-20230302152338277](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302152338277.png)

# 测试组件库

1. npm 安装组件

2. 然后导入使用

   ```vue
   <template>
     <z-button />
   </template>
   <script setup>
   import { zButton } from "v3-zy-ui";
   </script>
   ```

   如果样式没有加载就在 main.ts 中导入组件的样式文件

   `import "../node_modules/v3-zy-ui/dist/style.css";`

   显示出组件就没问题了，下面就自己开发自己的组件把
