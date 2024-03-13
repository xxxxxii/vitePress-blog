<template>
    <header>
        <div class="logo">
            <div class="logo-icon" style="display: flex;align-items: end;">
                <!-- <img src="../../../public/horse.png" style="width: 50px;" /> -->
                <div
                    style="display: flex;margin-bottom: 2px;align-items: center;justify-content: center;width: 22px;height: 22px;border-radius: 4px; background:var(--vp-c-important-1); color: beige;">
                    Hi
                </div>
                <div style="margin:0 0 0 10px;">
                    {{ site.title }}
                </div>
            </div>



            <button v-if="false" aria-label="Open Menu" class="hamburger-menu focus-outline" aria-controls="menu-items"
                aria-expanded="1">
                <svg class="menu-icon svelte-4y4p7p" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 26 26"
                    xmlns:xlink="http://www.w3.org/1999/xlink" fill="none" height="26" stroke="currentColor"
                    stroke-linecap="round" stroke-linejoin="round" stroke-width="1" width="26">
                    <g fill="none">
                        <path
                            d="M16 4c1.104-.019 2 .896 2 2v8a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h12zm1 2a1 1 0 0 0-1-1h-2.995v10H16a1 1 0 0 0 1-1V6zm-4.995 9V5H4.001a1 1 0 0 0-1 1v8a1 1 0 0 0 1 1h8.004z"
                            fill="currentColor"></path>
                    </g>
                </svg>
            </button>
        </div>
        <VPNavBarSearch style="padding: 0 6px;" />
        <ul style="margin-bottom: 5px;">
            <li v-for="item in theme.nav" :key="item.link">
                <a :href="item.link">{{ item.text }}</a>
            </li>
            <li style="display: flex;">
                <a v-for="item in theme.socialLinks" :key="item.link" :href="item.link" v-html="item.icon.svg">
                </a>
            </li>

            <!-- <li>
                <a href="#">
                    <VPSwitchAppearance />
                </a>
            </li> -->
        </ul>

        <div style="width: 100%; color: var(--vp-c-text-1); position: absolute; bottom: 5px;">
            <button style="padding: 8px;" @click="showToolsBox($event)">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="var(--vp-c-text-1)" width="16"
                    height="16">
                    <path
                        d="M1.5 3.25c0-.966.784-1.75 1.75-1.75h2.5c.966 0 1.75.784 1.75 1.75v2.5A1.75 1.75 0 0 1 5.75 7.5h-2.5A1.75 1.75 0 0 1 1.5 5.75Zm7 0c0-.966.784-1.75 1.75-1.75h2.5c.966 0 1.75.784 1.75 1.75v2.5a1.75 1.75 0 0 1-1.75 1.75h-2.5A1.75 1.75 0 0 1 8.5 5.75Zm-7 7c0-.966.784-1.75 1.75-1.75h2.5c.966 0 1.75.784 1.75 1.75v2.5a1.75 1.75 0 0 1-1.75 1.75h-2.5a1.75 1.75 0 0 1-1.75-1.75Zm7 0c0-.966.784-1.75 1.75-1.75h2.5c.966 0 1.75.784 1.75 1.75v2.5a1.75 1.75 0 0 1-1.75 1.75h-2.5a1.75 1.75 0 0 1-1.75-1.75ZM3.25 3a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2.5A.25.25 0 0 0 6 5.75v-2.5A.25.25 0 0 0 5.75 3Zm7 0a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2.5a.25.25 0 0 0 .25-.25v-2.5a.25.25 0 0 0-.25-.25Zm-7 7a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2.5a.25.25 0 0 0 .25-.25v-2.5a.25.25 0 0 0-.25-.25Zm7 0a.25.25 0 0 0-.25.25v2.5c0 .138.112.25.25.25h2.5a.25.25 0 0 0 .25-.25v-2.5a.25.25 0 0 0-.25-.25Z">
                    </path>
                </svg>
            </button>
        </div>
    </header>

    <dialog id="g-dialog" :open="tools.show" @click="$event.stopPropagation()">
        <div style="display: flex;flex-wrap: wrap;">
            <div class="item-p" style="display: flex; align-items: center;width: 100%;">
                <audio id="music" controls :src="tools.musicUrl"></audio> <span style="cursor: pointer;"
                    @click="getMusic">下一首</span>
            </div>
            <div>
                <!-- <video></video> -->
            </div>
            <div class="item-p" style="width: 100%;">
                <VPSwitchAppearance />
                <div>
                    <span v-if="user">当前系统环境: {{ user?.system + ' ' + user?.browser }}</span>
                </div>
            </div>

        </div>
    </dialog>
</template>

<script setup>
import { useData, withBase } from "vitepress";
import {ref} from "vue"

// import { nav } from "../../menu";
import VPNavBarSearch from './VPNavBarSearch.vue'
import VPSwitchAppearance from './VPSwitchAppearance.vue'

const { theme ,site } = useData();

let tools= ref({
    show:false,
    musicUrl:null
})
let user = ref({
    sys:{}
})

function showToolsBox(e){
    tools.value.show = !tools.value.show 
    e.stopPropagation()
}

function getMusic() {
  fetch('https://api.qqsuu.cn/api/dm-randmusic?sort=%E7%83%AD%E6%AD%8C%E6%A6%9C&format=json').then((response) => {
    // 判断响应状态为200表示请求成功
    if (response.ok) {
      return response.json(); // 将响应转换为JSON格式
    } else {
      throw new Error('Network response was not ok'); // 若不是200则抛出错误
    }
  })
    .then((data) => {
      tools.value.musicUrl = data.data.url
    })
    .catch((error) => {
      console.error('Error:', error); // 输出错误信息
    });
}

function getUserSys(){
    fetch('https://api.qqsuu.cn/api/dm-visitor').then((response) => {
    // 判断响应状态为200表示请求成功
    if (response.ok) {
      return response.json(); // 将响应转换为JSON格式
    } else {
      throw new Error('Network response was not ok'); // 若不是200则抛出错误
    }
  })
    .then((data) => {
      user.value = data
    })
    .catch((error) => {
      console.error('Error:', error); // 输出错误信息
    });
}

getMusic();
getUserSys();


window.addEventListener('click',function(){
    tools.value.show = false
})
</script>

<style scoped>
header {
    z-index: 9999;
    width: 100%;
}

.logo {
    display: flex;
    padding: 8px;
}

.logo>.logo-icon {
    flex: 1;
}

.hamburger-men {
    flex: none;
}

ul {
    padding: 8px;
}

ul>li>a {
    padding: 4px;
}

a {
    display: block;
}

.icon {
    color: #000;
}

@media (max-width: 960px) {
    header {
        display: none;
    }
}

.item-p {
    padding: 8px;
}

dialog {
    position: fixed;
    border: none;
    border-radius: 8px;
    top: 40%;
    max-width: 640px;
    z-index: 9999;
}

@media (min-width: 960px) {
    dialog {
        max-width: 100%;
    }
}


dialog::backdrop {
    position: fixed;
    top: 0px;
    right: 0px;
    bottom: 0px;
    left: 0px;
    background: rgba(0, 0, 0, 0.1);
}
</style>
