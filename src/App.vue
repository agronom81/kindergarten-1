<template>
  <main class="w-[958px] mx-auto relative">
    <div class="flex justify-center items-center relative fade-in">
      <img class="block m-0" src="./assets/img/photo1.jpg" alt="image" />
      <DotItem top="450px" left="577px" :content="dotContent.item1"></DotItem>
      <DotItem top="587px" left="764px" :content="dotContent.item2"></DotItem>
      <DotItem top="618px" left="478px" :content="dotContent.item3"></DotItem>
      <DotItem top="424px" left="141px" :content="dotContent.item4"></DotItem>
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
import windJpeg from "./assets/img/wind.jpeg";
import flowersJpeg from "./assets/img/board.png";
import calendarJpeg from "./assets/img/board2.png";
import flugerJpeg from "./assets/img/fluger.jpeg";
const dotContent = ref({
  item1: {
    label: "Вітряний рукав",
    imgPath: windJpeg,
    sound: wind,
  },
  item2: {
    label: "Квітник",
    imgPath: flowersJpeg,
    sound: flowers,
  },
  item3: {
    label: "Погода",
    imgPath: calendarJpeg,
    sound: calendar,
  },
  item4: {
    label: "Флюгер",
    imgPath: flugerJpeg,
    sound: fluger,
  },
});
</script>

<style scoped></style>
