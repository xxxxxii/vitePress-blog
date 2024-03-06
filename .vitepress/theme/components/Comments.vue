<template>
  <div id="gitalk-container"></div>
</template>

<script lang="ts" setup>
import "gitalk/dist/gitalk.css";
import Gitalk from "gitalk";
import { onContentUpdated, useRouter } from "vitepress";

// const { route, go } = useRouter();
function deleteChild(element: HTMLDivElement | null) {
  let child = element?.lastElementChild;
  while (child) {
    element?.removeChild(child);
    child = element?.lastElementChild;
  }
}
onContentUpdated(() => {
  // reset gittalk element for update
  const element = document.querySelector("#gitalk-container");
  if (!element) {
    return;
  }
  deleteChild(element);
  const gitalk = new Gitalk({
    clientID: "ef6e085c5f4e69c987d0",
    clientSecret: "e9d02278a1295be94fc6a946e5e2ad778e5dd3bb",
    repo: "gitalk-comments",
    owner: "xxxxxii",
    admin: ["xxxxxii"],
    id: location.pathname.substring(0, 50), // Ensure uniqueness and length less than 50
    language: "zh-CN",
    distractionFreeMode: false, // Facebook-like distraction free mode
  });
  gitalk.render("gitalk-container");
});
</script>

<style scoped></style>
