<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const props = defineProps({
  src: String,
  alt: {
    type: String,
    default: "",
  },
});

const imageRef = ref(null);
const observer = ref(null);
const loaded = ref(false);
const realSrc = ref(""); // actual API call will happen only when visible

onMounted(() => {
  observer.value = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      realSrc.value = props.src; // set src only when the screen is visible
      loaded.value = true;
      observer.value.disconnect();
    }
  });

  if (imageRef.value) {
    observer.value.observe(imageRef.value);
  }
});

onBeforeUnmount(() => {
  if (observer.value) observer.value.disconnect();
});
</script>

<template>
  <div ref="imageRef" class="image-container">
    <img
      v-if="loaded"
      :src="realSrc"
      :alt="alt"
      class="fade-in"
    />
    <div v-else class="placeholder">Loading...</div>
  </div>
</template>

<style scoped>
.image-container {
  width: 100%;
  min-height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 16px;
  background: #f5f5f5;
  border-radius: 8px;
}
.placeholder {
  color: #999;
  font-size: 14px;
}
.fade-in {
  width: 100%;
  height: auto;
  border-radius: 8px;
  animation: fadeIn 1s ease-in;
}
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
