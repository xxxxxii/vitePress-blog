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
        <VPNavBarSearch />
        <ul>
            <li v-for="item in theme.nav" :key="item.link">
                <a :href="item.link">{{ item.text }}</a>
            </li>
            <li style="display: flex;">
                <a v-for="item in theme.socialLinks" :key="item.link" :href="item.link" v-html="item.icon.svg">
                </a>
            </li>
            <li>
                <a href="#">
                    <VPSwitchAppearance />
                </a>
            </li>
        </ul>
    </header>
</template>

<script setup>
import { useData, withBase } from "vitepress";

// import { nav } from "../../menu";
import VPNavBarSearch from './VPNavBarSearch.vue'
import VPSwitchAppearance from './VPSwitchAppearance.vue'

const { theme ,site } = useData();
// console.log(useData())
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
