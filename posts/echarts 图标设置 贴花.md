---
author: yulinZ
date: 2023-09-05
title: echarts 中图表设置贴花
postSlug: echarts 中图表设置贴花
featured: false
draft: false
tags:
  - 前端
  - 日常笔记
  - echarts
ogImage: ""
description: echarts & 贴花
---

# echarts 图标设置 贴花

- 重点： echarts 版本需要在 5.0 及以上(低版本也可以实现，限制条件比较多和复杂)

## aria 属性

为系列数据增加贴花纹理，作为颜色的辅助，帮助区分数据。使用默认贴花图案的方式非常简单，只需要开启即可：

```js
 aria: {
    enabled: true,
    decal: {
        show: true
    }
 },
```

![](https://gitee.com/yulinzhu/pic-window/raw/master//ffd36ccde409005c085cccb00edc8817.png)
完整代码：

```js
option = {
  tooltip: {
    trigger: "item",
  },
  legend: {
    top: "5%",
    left: "center",
  },
  aria: {
    enabled: true,
    decal: {
      show: true,
    },
  },
  series: [
    {
      name: "Access From",
      type: "pie",
      radius: ["40%", "70%"],
      avoidLabelOverlap: false,
      itemStyle: {
        borderRadius: 10,
        borderColor: "#fff",
        borderWidth: 2,
      },
      label: {
        show: false,
        position: "center",
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 40,
          fontWeight: "bold",
        },
      },
      labelLine: {
        show: false,
      },
      data: [
        { value: 1048, name: "Search Engine" },
        { value: 735, name: "Direct" },
        { value: 580, name: "Email" },
        { value: 484, name: "Union Ads" },
        { value: 300, name: "Video Ads" },
      ],
    },
  ],
};
```

## 默认贴花类型

可以在 decal 中通过 symbol 去设置
symbol
该属性是配置贴花的图案，数据类型可以是 string，也可以是 string[]
一共有四种数据可以选择

1. 官方提供的贴花图案
2. 使用图片 http 地址： symbol: `image://https://www.mercedes-benz.com.cn/content/dam/mb-cn/renovation/300_0415.png`,
3. 使用图片 dataURI 地址：symbol: `image://data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7`,

4. 使用 path://将图标设置为任意的矢量路径：symbol: 'path://M30.9,53.2C16.8,53.2,5.3,41.7,5.3,27.6S16.8,2,30.9,2C45,2,56.4,13.5,56.4,27.6S45,53.2,30.9,53.2z M30.9,3.5C17.6,3.5,6.8,14.4,6.8,27.6c0,13.3,10.8,24.1,24.101,24.1C44.2,51.7,55,40.9,55,27.6C54.9,14.4,44.1,3.5,30.9,3.5z M36.9,35.8c0,0.601-0.4,1-0.9,1h-1.3c-0.5,0-0.9-0.399-0.9-1V19.5c0-0.6,0.4-1,0.9-1H36c0.5,0,0.9,0.4,0.9,1V35.8z M27.8,35.8 c0,0.601-0.4,1-0.9,1h-1.3c-0.5,0-0.9-0.399-0.9-1V19.5c0-0.6,0.4-1,0.9-1H27c0.5,0,0.9,0.4,0.9,1L27.8,35.8L27.8,35.8z',
   dashArrayX: [20, 10, 20, 10 ],
   dashArrayY: [20, 10, 20, 10 ],

```js
 aria: {
    enabled: true,
    decal: {
        symbol: 'react'
    }
  },
```

如果每一块数据需要单独设置可以这样

```js
aria:{
    enabled:true,
    decal:{
        show: true,
        decals: [
            {symbol: 'rect'},
            {symbol: 'circle'},
            {symbol: 'roundRect'},
            {symbol: 'triangle'},
            {symbol: 'diamond'},
            {symbol: 'pin'},
            {symbol: 'arrow'}
        ]
    }
}
```

![](https://gitee.com/yulinzhu/pic-window/raw/master//ffd36ccde409005c085cccb00edc8817.png)
更多详情可以去看官方的配置文档

## 低版本设置贴花

网上找到的方法好像只有通过添加贴图的方式

```js
var barImage =
  "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC4AAADwCAYAAAB/***";
var PatternImgA = new Image();
PatternImgA.src = barImage;
series: [
  {
    name: "**",
    type: "bar",
    yAxisIndex: 0,
    data: [
      {
        value: 198,
        itemStyle: {
          color: {
            image: PatternImgA, // 设置贴花的图片
            repeat: "repeat",
          },
        },
      },
    ],

    label: {
      normal: {
        show: true, //开启显示
        position: "top", //柱形上方
        textStyle: {
          //数值样式
          color: "#fff",
        },
      },
    },
  },
  {
    name: "***",
    type: "bar",
    yAxisIndex: 0,
    data: cData2,
    label: {
      normal: {
        show: true, //开启显示
        position: "inside", //柱形上方
        textStyle: {
          //数值样式
          color: "#000000",
        },
        formatter: params => {
          return params.data.value + " %";
        },
      },
    },
  },
];
```
