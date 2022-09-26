<template>
  <div
    class="absolute w-8 h-8 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="block w-52 h-24 bg-white shadow-2xl p-2 top-[-5rem] left-[-12rem] opacity-80 rounded-md"
    >
      <p>Lorem ipsum dolor sit.</p>
    </div>
    <button
      @click="showPopUp"
      class="absolute top-[50%] left-[50%] translate-x-[-50%] hover:w-8 hover:h-8 transition-all translate-y-[-50%] w-6 h-6 bg-white cursor-pointer rounded-full"
      type="button"
    ></button>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
defineProps<{
  top: string;
  left: string;
}>();

const isShow = ref(false);
function showPopUp() {
  isShow.value = !isShow.value;
}
</script>

<style scoped>
.dotItem {
  top: 20px;
  left: 20px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
</style>
