<template>
  <main>
    <div class="w-[958px] mx-auto relative">
      <div class="mx-auto relative table fade-in">
        <img class="block m-0" src="./assets/photo1.jpg" alt="image" />
        <DotItem top="450px" left="579px" :content="dotContent.item1"></DotItem>
        <DotItem top="587px" left="766px" :content="dotContent.item1"></DotItem>
        <DotItem top="707px" left="480px" :content="dotContent.item1"></DotItem>
        <DotItem top="424px" left="144px" :content="dotContent.item1"></DotItem>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";
import DotItem from "./components/DotItem.vue";
const dotContent = ref({
  item1: {
    label: "Lorem",
    description: "ipsum dolor sit amet consectetur adipisicing elit",
  },
});
</script>

<style scoped></style>
