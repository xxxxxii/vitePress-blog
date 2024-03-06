<template>
    <header>

        <div class="logo">
            <div class="logo-icon">
                <img src="../../../public/horse.svg" />
            </div>
            <button aria-label="Open Menu" class="hamburger-menu focus-outline" aria-controls="menu-items"
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
        <VPNavBarSearch />
        <ul>

            <li v-for="item in nav" :key="item.link">
                <a :href="item.link">{{ item.text }}</a>
            </li>
            <li>
                <a href="#">
                    <VPSwitchAppearance />
                </a>
            </li>
            <!-- <li>
                <a href="#">
                    <button data-v-7232ffcd="" data-v-61f3123e="" data-v-456ede54="" class="VPSwitch VPSwitchAppearance"
                        type="button" role="switch" title="Switch to dark theme" aria-checked="true"
                        @click="switchTheme($event)">
                        <span data-v-7232ffcd="" class="check"><span data-v-7232ffcd="" class="icon"><svg
                                    data-v-61f3123e="" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"
                                    focusable="false" viewBox="0 0 24 24" class="sun">
                                    <path
                                        d="M12,18c-3.3,0-6-2.7-6-6s2.7-6,6-6s6,2.7,6,6S15.3,18,12,18zM12,8c-2.2,0-4,1.8-4,4c0,2.2,1.8,4,4,4c2.2,0,4-1.8,4-4C16,9.8,14.2,8,12,8z">
                                    </path>
                                    <path d="M12,4c-0.6,0-1-0.4-1-1V1c0-0.6,0.4-1,1-1s1,0.4,1,1v2C13,3.6,12.6,4,12,4z">
                                    </path>
                                    <path
                                        d="M12,24c-0.6,0-1-0.4-1-1v-2c0-0.6,0.4-1,1-1s1,0.4,1,1v2C13,23.6,12.6,24,12,24z">
                                    </path>
                                    <path
                                        d="M5.6,6.6c-0.3,0-0.5-0.1-0.7-0.3L3.5,4.9c-0.4-0.4-0.4-1,0-1.4s1-0.4,1.4,0l1.4,1.4c0.4,0.4,0.4,1,0,1.4C6.2,6.5,5.9,6.6,5.6,6.6z">
                                    </path>
                                    <path
                                        d="M19.8,20.8c-0.3,0-0.5-0.1-0.7-0.3l-1.4-1.4c-0.4-0.4-0.4-1,0-1.4s1-0.4,1.4,0l1.4,1.4c0.4,0.4,0.4,1,0,1.4C20.3,20.7,20,20.8,19.8,20.8z">
                                    </path>
                                    <path d="M3,13H1c-0.6,0-1-0.4-1-1s0.4-1,1-1h2c0.6,0,1,0.4,1,1S3.6,13,3,13z"></path>
                                    <path d="M23,13h-2c-0.6,0-1-0.4-1-1s0.4-1,1-1h2c0.6,0,1,0.4,1,1S23.6,13,23,13z">
                                    </path>
                                    <path
                                        d="M4.2,20.8c-0.3,0-0.5-0.1-0.7-0.3c-0.4-0.4-0.4-1,0-1.4l1.4-1.4c0.4-0.4,1-0.4,1.4,0s0.4,1,0,1.4l-1.4,1.4C4.7,20.7,4.5,20.8,4.2,20.8z">
                                    </path>
                                    <path
                                        d="M18.4,6.6c-0.3,0-0.5-0.1-0.7-0.3c-0.4-0.4-0.4-1,0-1.4l1.4-1.4c0.4-0.4,1-0.4,1.4,0s0.4,1,0,1.4l-1.4,1.4C18.9,6.5,18.6,6.6,18.4,6.6z">
                                    </path>
                                </svg>
                                <svg data-v-61f3123e="" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"
                                    focusable="false" viewBox="0 0 24 24" class="moon">
                                    <path
                                        d="M12.1,22c-0.3,0-0.6,0-0.9,0c-5.5-0.5-9.5-5.4-9-10.9c0.4-4.8,4.2-8.6,9-9c0.4,0,0.8,0.2,1,0.5c0.2,0.3,0.2,0.8-0.1,1.1c-2,2.7-1.4,6.4,1.3,8.4c2.1,1.6,5,1.6,7.1,0c0.3-0.2,0.7-0.3,1.1-0.1c0.3,0.2,0.5,0.6,0.5,1c-0.2,2.7-1.5,5.1-3.6,6.8C16.6,21.2,14.4,22,12.1,22zM9.3,4.4c-2.9,1-5,3.6-5.2,6.8c-0.4,4.4,2.8,8.3,7.2,8.7c2.1,0.2,4.2-0.4,5.8-1.8c1.1-0.9,1.9-2.1,2.4-3.4c-2.5,0.9-5.3,0.5-7.5-1.1C9.2,11.4,8.1,7.7,9.3,4.4z">
                                    </path>
                                </svg></span></span>
                    </button>
                </a>
            </li> -->
        </ul>
    </header>
</template>

<script setup>
import { useData, withBase } from "vitepress";



import { nav } from "../../menu";
import VPNavBarSearch from 'vitepress/dist/client/theme-default/components/VPNavBarSearch.vue'
import VPSwitchAppearance from 'vitepress/dist/client/theme-default/components/VPSwitchAppearance.vue'
// let gTheme = localStorage.getItem("vitepress-theme-appearance");
// let htmlDom = document.querySelector("html");


const { theme  } = useData();


// function switchTheme(e) {
//   let curTheme = localStorage.getItem("vitepress-theme-appearance");
//   if (curTheme === "dark") {
//     htmlDom.classList.remove("dark");
//     htmlDom.classList.add("auto");
//     localStorage.setItem("vitepress-theme-appearance", "auto");
//   } else {
//     htmlDom.classList.remove("auto");
//     htmlDom.classList.add("dark");
//     localStorage.setItem("vitepress-theme-appearance", "dark");
//   }
// }
</script>

<style scoped>
header {
    border-right: 1px solid var(--vp-code-block-divider-color);
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
</style>
