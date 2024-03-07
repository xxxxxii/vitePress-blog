---
author: yulinZ
date: 2023-09-05
title: vue v-model 原理
postSlug: vue v-model 原理
featured: true
draft: false
tags:
  - 前端
  - vue
  - 日常笔记
ogImage: ""
description: vue v-model 原理
---

# vue v-model 原理

v-model 其实是 vue 语法的一个语法糖

## vue 中不用 v-model 怎样去实现数据的双向绑定

用 v-bind 动态去绑定属性值，然后监听 input 事件，事件修改把值赋给绑定的变量。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>v-model</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.min.js"></script>
  </head>
  <body>
    <div id="app">
      <input v-bind:value="inputValue" v-on:input="input" />
      {{inputValue}}
    </div>
    <script>
      new Vue({
        el: "#app",
        data() {
          return {
            inputValue: "hello",
          };
        },
        methods: {
          input(e) {
            console.log(e.target.value);
            this.inputValue = e.target.value;
          },
        },
      });
    </script>
  </body>
</html>
```

## 底层实现其实是基于 vue 的核心数据响应式

下面简单的实现一下，使用`Object.defineProperty`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>v-model</title>
  </head>
  <body>
    <input type="text" id="input" />

    <script>
      let obj = {
        inputValue: "",
      };
      let inputDom = document.querySelector("#input");

      // 侦听数据变化，修改input 的值
      Object.defineProperty(obj, "inputValue", {
        enumerable: true, //可枚举
        configurable: true, // 可改变
        get: function () {
          console.log("读取值");
          return obj["inputValue"];
        },
        set: function (newVal) {
          console.log("设置值");
          inputDom.value = newVal;
        },
      });

      // 监听 input 的 input事件
      inputDom.addEventListener("input", e => {
        console.log(inputDom.value);
        obj.inputValue = inputDom.value;
      });

      obj.inputValue = "初始值111";
    </script>
  </body>
</html>
```

同样给 input 添加 input 监听事件，改变了就把值赋给一个对象中的属性，用 Object.defineProperty 去侦听这个对象中的属性，一旦监测到值改变了就把值赋值给 input dom 的 value 属性
