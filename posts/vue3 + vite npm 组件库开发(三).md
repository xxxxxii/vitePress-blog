---
author: yulinZ
pubDatetime: 2023-09-05
title: vue3 + vite npm 组件库开发(三)
postSlug: vue3 + vite npm 组件库开发(三)
featured: true
draft: false
tags:
  - 前端
  - vue
  - 日常笔记
ogImage: ""
description: vue3 + vite npm 组件库开发(三)
---

# vue3 + vite npm 组件库开发(三)

组件库编写文档可能会用到很多的 demo，很多的情况下，手动去引入太繁琐，如下图：

![image-20230302172319639](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302172319639.png)

![image-20230302172121237](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302172121237.png)

textarea 组件下 doc 有很多的 demo,那我就要在 index.md 文件中全部引入

# 编写一个脚本去实现自动生成 index.md 文件

本来想使用 python 去编写，但是都在相同环境下，就直接使用 node 了，相对要复杂一点，但也是 node 语法，逻辑都很简单

## 逻辑分析

1. 检索 packages 目录下的所以组件，如果 doc 下面不存在 index,md,这个组件的文档就需要初始化，存在就不用管它。
2. 根据 doc 下面的 vue 文件去生成对应的组件文档，有多少个 vue dome 就导入多少个，最后在导入一个显示代码的组件即可
3. 设置 dome 文件的命名规则，可以单个单词，也可以用短横线-去连接，驼峰命名也可

## 脚本代码

在项目根目录创建一个 js 文件 create-comp-md.js

代码如下：

```js
const fs = require("fs");

// directory path
const dir = "./packages/";

// script 中的代码
let str = "";

// 导入组件的使用代码
let str1 = "";

// list all files in the directory
fs.readdir(dir, (err, files) => {
  if (err) {
    throw err;
  }
  // files object contains all files names
  // log them on console
  // 循环packages下面的文件
  files.forEach(file => {
    fs.stat(dir + file, function (err, stats) {
      // true || false 判断是不是文件夹，文件夹就是doc目录，也可以直接去读取doc下的文件
      if (stats.isDirectory()) {
        fs.readdir(dir + file + "/doc/", (err, Dfiles) => {
          if (err) {
            throw err;
          }
          // 判断是否存在'index.md'文件，不存在就去生成
          if (!Dfiles.includes("index.md")) {
            Dfiles.forEach(item => {
              console.log("item", item);
              // 判断是否是vue文件，vue文件才去导入
              let vueFName = item.split(".");
              if (vueFName[1] === "vue") {
                // 处理导入的组件名称
                // 没有-连接符就直接使用文件名，有-需要转成驼峰例如 demo-text->demoText
                let compName = "";
                if (item.indexOf("-") !== -1) {
                  let items = vueFName[0].split("-");
                  console.log(items);
                  compName =
                    items[0] +
                    items[1].slice(0, 1).toUpperCase() +
                    items[1].slice(1).split(".")[0];
                } else {
                  compName = item.split(".")[0];
                }
                // 设置要生成的字符串
                str += `\n  import ${compName} from "./${item}"`;
                str1 += `\n<${compName} />\n<pre-view compName="${file}" vueFName="${vueFName[0]}" />\n`;
              }
            });
            // 2段字符串拼接
            str =
              `# ${
                file.slice(0, 1).toUpperCase() + file.slice(1)
              } 组件\n<script setup>` +
              str +
              `\n  import preView from "@/components/preview/preview.vue"` +
              `\n</script>`;

            // 生成md文件并写入
            fs.writeFile(
              dir + file + "/doc/" + `index.md`,
              str + str1,
              function (err) {
                if (err) {
                  throw err;
                }
                console.log("write over");
              }
            );
            console.log(str + str1);
          }
        });
      }
    });
  });
});
```

## 测试脚本

packages 下新建

![image-20230302175046024](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302175046024.png)

执行脚本 node ./create-comp-md.js doc 下会生成 index.md 文件，查看文件是否生成正确

```vue
# Test 组件
<script setup>
import demoTest from "./demo-test.vue";
import demo from "./demo.vue";
import demoStr from "./demoStr.vue";
import preView from "@/components/preview/preview.vue";
</script>
<demoTest />
<pre-view compName="test" vueFName="demo-test" />

<demo />
<pre-view compName="test" vueFName="demo" />

<demoStr />
<pre-view compName="test" vueFName="demoStr" />
```

再配置路由显示即可

![image-20230302175737913](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230302175737913.png)

页面正常渲染

# 总结

我们只需要去关注.vue demo 文件即可，每次开发完组件执行就行了，然会再去编写文档，就不用去导入组件耗费时间
