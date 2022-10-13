<template>
  <main class="w-[958px] mx-auto relative h-screen">
    <div class="flex justify-center items-center relative fade-in h-screen">
      <img class="block m-0" src="./assets/img/photo1.jpg" alt="image" />
      <DotItem top="450px" left="579px" :content="dotContent.item1"></DotItem>
      <DotItem top="587px" left="766px" :content="dotContent.item2"></DotItem>
      <DotItem top="618px" left="480px" :content="dotContent.item3"></DotItem>
      <DotItem top="424px" left="144px" :content="dotContent.item4"></DotItem>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import DotItem from "./components/DotItem.vue";
import calendar from "./assets/audio/calendar.mp3";
import flowers from "./assets/audio/flowers.mp3";
import fluger from "./assets/audio/fluger.mp3";
import wind from "./assets/audio/wind.mp3";
const dotContent = ref({
  item1: {
    label: "Вітряний рукав",
    imgPath: "/src/assets/img/wind.jpeg",
    sound: wind,
  },
  item2: {
    label: "Квітник",
    imgPath: "/src/assets/img/board.png",
    sound: flowers,
  },
  item3: {
    label: "Погода",
    imgPath: "/src/assets/img/board2.png",
    sound: calendar,
  },
  item4: {
    label: "Флюгер",
    imgPath: "/src/assets/img/fluger.jpeg",
    sound: fluger,
  },
});
</script>

<style scoped></style>
