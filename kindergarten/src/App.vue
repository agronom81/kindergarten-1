<template>
  <main>
    <div class="w-[958px] mx-auto relative">
      <div class="mx-auto relative table fade-in">
        <img class="block m-0" src="./assets/img/photo1.jpg" alt="image" />
        <DotItem top="450px" left="579px" :content="dotContent.item1"></DotItem>
        <DotItem top="587px" left="766px" :content="dotContent.item2"></DotItem>
        <DotItem top="707px" left="480px" :content="dotContent.item3"></DotItem>
        <DotItem top="424px" left="144px" :content="dotContent.item4"></DotItem>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import DotItem from "./components/DotItem.vue";
import calendar from "./assets/audio/calendar.m4a";
import flowers from "./assets/audio/flowers.m4a";
import fluger from "./assets/audio/fluger.m4a";
import wind from "./assets/audio/wind.m4a";
const dotContent = ref({
  item1: {
    label: "Вітряний рукав",
    imgPath: "/src/assets/img/wind.jpeg",
    description: "ipsum dolor sit amet consectetur adipisicing elit",
    sound: wind,
  },
  item2: {
    label: "Квітник",
    imgPath: "/src/assets/img/board.png",
    description: "ipsum dolor sit amet consectetur adipisicing elit",
    sound: flowers,
  },
  item3: {
    label: "Погода",
    imgPath: "/src/assets/img/board2.png",
    description: "ipsum dolor sit amet consectetur adipisicing elit",
    sound: calendar,
  },
  item4: {
    label: "Флюгер",
    imgPath: "/src/assets/img/fluger.jpeg",
    description: "ipsum dolor sit amet consectetur adipisicing elit",
    sound: fluger,
  },
});
</script>

<style scoped></style>
