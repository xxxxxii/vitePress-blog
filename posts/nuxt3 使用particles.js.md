---
author: yulinZ
date: 2023-09-05
title: nuxt3 使用particles.js
postSlug: nuxt3 使用particles.js
featured: false
draft: false
tags:
  - 前端
  - js
  - 日常笔记
ogImage: ""
description: nuxt3 使用particles.js
---

**nuxt3 使用 particles.js**

# 简介

[官方文档](https://particles.js.org/)

particles.js 是一个轻量级的创建粒子背景的 JavaScript 库，

# 安装

`npm install particles.vue3`

安装依赖模块

`npm install tsparticles`

# 使用

## 注册

如果是 vue 需要在 main.js 中导入，然而 nuxt3 不是 spa,没有 main.js 的文件。要在 plugins 中注册。

/plugins/particles.js

```ts
import { defineNuxtPlugin } from "#app";
import Particles from "particles.vue3";

export default defineNuxtPlugin(nuxtApp => {
  nuxtApp.vueApp.use(Particles);
});
```

## 页面使用

```vue
<template>
  <div>
    <Particles
      id="tsparticles"
      :particlesInit="particlesInit"
      :particlesLoaded="particlesLoaded"
      :options="options"
    />
  </div>
</template>
<script setup lang="ts">
import { reactive } from "vue";
import { loadFull } from "tsparticles";
import type { Engine } from "tsparticles-engine";

const particlesInit = async (engine: Engine) => {
  await loadFull(engine);
};

const particlesLoaded = async (container: any) => {
  console.log("Particles container loaded", container);
};
const options = reactive({
  background: {
    color: {
      value: "#fff", // 背景颜色
    },
  },
  fpsLimit: 60,
  interactivity: {
    events: {
      onClick: {
        enable: true,
        mode: "push", // 可用的click模式有: "push", "remove", "repulse", "bubble"。
      },
      onHover: {
        enable: true,
        mode: "grab", // 可用的hover模式有: "grab", "repulse", "bubble"。
      },
      resize: true,
    },
    modes: {
      bubble: {
        distance: 400,
        duration: 2,
        opacity: 0.8,
        size: 40,
      },
      push: {
        quantity: 4,
      },
      repulse: {
        distance: 200,
        duration: 0.4,
      },
    },
  },
  particles: {
    color: {
      value: ["#2EB67D", "#ECB22E", "#E01E5B", "#36C5F0"], // 粒子颜色
    },
    links: {
      color: "#969696", // '#dedede'。线条颜色。
      distance: 150, // 线条长度
      enable: true, // 是否有线条
      opacity: 0.5, // 线条透明度。
      width: 1, // 线条宽度。
    },
    collisions: {
      enable: false,
    },
    move: {
      direction: "none",
      enable: true,
      outMode: "bounce",
      random: false,
      speed: 2, // 粒子运动速度。
      straight: false,
    },
    number: {
      density: {
        enable: true,
        area: 800,
      },
      value: 80, // 粒子数量。
    },
    opacity: {
      value: 0.9, // 粒子透明度。
    },
    shape: {
      type: ["circle", "edge", "triangle", "polygon", "star"], // 可用的粒子外观类型有："circle","edge","triangle", "polygon","star"
    },
    size: {
      random: true,
      value: 5,
    },
  },
  detectRetina: true,
});
</script>
```

## 效果

![image-20230226190205101](https://gitee.com/yulinzhu/pic-window/raw/master/image-20230226190205101.png)

更多效果查阅[官方文档](https://particles.js.org/)
