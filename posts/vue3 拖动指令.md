---
author: yulinZ
pubDatetime: 2023-09-05
title: vue3 拖动指令
postSlug: vue3 拖动指令
featured: true
draft: false
tags:
  - 前端
  - js
  - 日常笔记
ogImage: ""
description: vue3 拖动指令
---

# vue3 拖动指令

## 实现条件

拖动不能超出边界

## 代码

在 src/directives/drag/index.ts 中

```js
export default {
  install(app: any) {
    defaneDrag(app);
  },
};

const defaneDrag = (app: {
  directive: (arg0: string, arg1: { mounted(el: any): void }) => void,
}) => {
  app.directive("drag", {
    mounted(el) {
      // 获取可移动元素的父节点
      let parentNode = el.parentNode;
      // 设置父节点定位
      parentNode.style.position = "relative";
      el.style.position = "absolute";

      // 设置鼠标hover效果:移动上前去显示可移动的提示效果，并且禁用页面可选择，离开恢复正常
      el.onmouseover = () => {
        el.style.cursor = "move";
      };
      el.onmouseout = () => {
        el.style.cursor = "none";
      };
      // 防止选中移动块上的文字等
      parentNode.onmouseover = () => {
        document.onselectstart = () => {
          return false;
        };
      };
      parentNode.onmouseout = () => {
        document.onselectstart = () => {
          return true;
        };
      };

      el.onmousedown = (event: any) => {
        //event的兼容,同时得到clientX,的值
        var event = event || window.event;
        let x = event.clientX - el.offsetLeft;
        let y = event.clientY - el.offsetTop; //得到小段的偏移
        // 将移动事件绑定到 document 上，防止拖动过快脱离开
        document.onmousemove = (event: any) => {
          let xx = event.clientX - x; //当移动的时候，用它的鼠标值减去偏移量
          let yy = event.clientY - y;
          if (xx <= 0) {
            //判定边界值 0，就在最边上了,
            xx = 0;
          }
          if (xx >= parentNode.offsetWidth - el.offsetWidth) {
            //大于整个盒子的宽度-小盒子的宽度
            xx = parentNode.offsetWidth - el.offsetWidth;
          }
          if (yy <= 0) {
            yy = 0;
          }
          if (yy >= parentNode.offsetHeight - el.offsetHeight) {
            yy = parentNode.offsetHeight - el.offsetHeight;
          }

          el.style.left = xx + "px";
          el.style.top = yy + "px";
        };
        el.onmouseup = () => {
          // 取消事件
          document.onmousemove = null;
          el.onmouseup = null;
        };
      };
    },
  });
};
```

## 使用

main.ts 添加

```js
import defaneDrag from "@/directives/drag";
app.use(defaneDrag);
```

页面使用

```html
<template>
  <div class="drag-box">
    <div class="rect" v-drag>拖动</div>
  </div>
</template>

<style scoped>
  .drag-box {
    width: 100%;
    height: 600px;
    background-color: aquamarine;
  }
  .rect {
    width: 100px;
    height: 100px;
    background-color: peru;
  }
</style>
```

## 实现效果

![image-20230217173120549](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230217173120549.png)
