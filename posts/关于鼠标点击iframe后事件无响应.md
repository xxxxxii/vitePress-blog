---
author: yulinZ
date: 2023-09-20
title: 关于鼠标点击iframe后事件无响应
postSlug: 关于鼠标点击iframe后事件无响应
featured: true
draft: false
tags:
  - 前端
  - js
  - html
  - 日常笔记
ogImage: ""
description: 关于鼠标点击iframe后事件无响应
---

# 发生条件

页面中嵌入 iframe 标签,当我们给页面添加了事件之后,鼠标点击到 ifarme 上,事件可能会失效

# 这里以全屏 iframe esc 退出为例

直接上代码

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        width: 100%;
        height: 100vh;
      }
      iframe {
        width: 100%;
        height: 100%;
        background: #969696;
      }
      #iframe-box {
        width: 60%;
        height: 50%;
      }
    </style>
  </head>
  <body>
    <div id="iframe-box">
      <iframe src=" " frameborder="0" id="iframe-dom"></iframe>
      <button onclick="fullScreen()">fullScreen</button>
    </div>

    <script>
      let iframe = null;
      iframe = document.getElementById("iframe-box");
      let isFull = false;
      function fullScreen() {
        // 全屏
        if (isFull) {
          iframe.style.width = "auto";
          iframe.style.height = "auto";
        } else {
          iframe.style.width = "100vw";
          iframe.style.height = "100vh";
        }
        isFull = !isFull;
      }

      // iframe = document.getElementById("iframe-dom");
      // let doc = iframe.contentWindow || iframe.contentDocument;
      //   doc.onkeydown = function (e) {
      //     if (e.keyCode == 27 && isFull) {
      //       fullScreen();
      //     }
      //   };
      window.onkeydown = function (e) {
        if (e.keyCode == 27 && isFull) {
          console.log(e);
          fullScreen();
        }
      };
    </script>
  </body>
</html>
```

当全屏后操作了 iframe 后 按 esc 会无响应,浏览器全局对象已经改变位 iframe 的了,所以需要给 iframe 添加键盘事件监听

```js
let iframe = document.getElementById("iframe-dom");
let doc = iframe.contentWindow || iframe.contentDocument;
doc.onkeydown = function (e) {
  if (e.keyCode == 27 && isFull) {
    fullScreen();
  }
};
```

`contentWindow || contentDocument` 可以获取到 iframe 的 window 和 document 对象,再添加事件监听即可

# 其他解决方案 postMessage

也可以通过 在 iframe 所在页面添加一个`onkeydown`事件,触发后发送信息到父级页面.
这种方法存在很多局限性,一般不推荐使用

1. 需要修改 iframe 页面代码
2. 如果嵌入的是第三方的页面,无权修改
