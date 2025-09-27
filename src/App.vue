<script setup>
import LazyImage from "./components/LazyImage.vue";

const images = [
  "https://picsum.photos/id/1015/600/400",
  "https://picsum.photos/id/1016/600/400",
  "https://picsum.photos/id/1018/600/400",
  "https://picsum.photos/id/1020/600/400",
  "https://picsum.photos/id/1024/600/400",
  "https://picsum.photos/id/1015/600/400",
  "https://picsum.photos/id/1016/600/400",
  "https://picsum.photos/id/1018/600/400",
  "https://picsum.photos/id/1020/600/400",
  "https://picsum.photos/id/1024/600/400"
];
</script>

<template>
  <h1>Vue 3 Lazy Loading Images (API call only when screen is visible)</h1>
  <div>
    <LazyImage
      v-for="(img, index) in images"
      :key="index"
      :src="img"
      :alt="`Image ${index + 1}`"
    />
  </div>
</template>

<style>
body {
  font-family: sans-serif;
  margin: 20px;
}
h1 {
  margin-bottom: 20px;
}
</style>
