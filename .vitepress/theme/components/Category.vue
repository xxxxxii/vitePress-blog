<template>
  <div class="category" id="catelogList">
  </div>
</template>

<script lang="ts" setup>
import { useData, onContentUpdated } from "vitepress";
import { shallowRef, ref, onMounted } from "vue";
import { getHeaders } from "../utils";
import katelog from 'katelog';

const { frontmatter, theme } = useData();
// const headers = shallowRef<any>([]);
const curIndex = ref(0);

onMounted(() => {
  let katelogIns = new katelog({
    contentEl: 'VPContent',
    catelogEl: 'catelogList',
    linkClass: 'k-catelog-link',
    linkActiveClass: 'k-catelog-link-active',
    supplyTop: 20,
    selector: ['h1', 'h2', 'h3', 'h4', 'h5', 'h6'],
    // active: function (el) {
    //   console.log(el);
    // }
  });
  katelogIns.rebuild();
})
// onContentUpdated(() => {
//   headers.value = getHeaders(frontmatter.value.outline ?? theme.value.outline);
//   console.log(headers.value)

//   // showIndent.value = headers.value.some((header) => {
//   //   return header.level === 2;
//   // });
// });
// function scrollTo(e, index, item) {
//   curIndex.value = index

//   let dom = document.querySelector(item?.link);
//   document.querySelector('#layout-content').scroll({
//     top: dom.offsetTop,
//     behavior: 'smooth'
//   });
// }
</script>

<style>
.k-catelog-link {
  position: relative;
  padding-top: 5px;
  padding-bottom: 5px;
  font-size: 14px;
  transition: all 0.5s;
}

.k-catelog-link::before {
  transition: all 0.5s;
}

.k-catelog-link-active {
  color: #1e80ff;
}

.k-catelog-link-active::before {
  content: "";
  position: absolute;
  top: 8px;
  left: -10px;
  width: 3px;
  height: 14px;
  background: #1e80ff;
  border-radius: 2px;
}
</style>

<style scoped>
.category {
  width: 20rem;
  background: var(--vp-c-bg);
  box-shadow: 6px 6px var(--vp-c-brand);
  border: 4px solid #3f4e4f;
  color: var(--vp-c-brand-light);
  overflow-y: auto;
  max-height: 300px;
  z-index: 999;
}

.list {
  padding-left: 1.25em;
  margin: 1rem 0;
  line-height: 1.7;
  list-style-type: none;
  box-sizing: border-box;
}

.showIndent {
  padding-left: 1rem;
}

ul {
  list-style-type: none;
}

.header {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

@media (min-width: 768px) {
  .category {
    max-height: 400px;
  }
}

@media (min-width: 1024px) {
  .category {
    max-height: 450px;
  }
}

@media (min-width: 1400px) {
  .category {
    position: fixed;
    right: 20px;
    max-height: 490px;
  }
}
</style>
