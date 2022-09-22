<template>
  <div class="absolute w-4 h-4 rounded-full">
    <button
      class="absolute w-full h-full top-0 left-0 bg-white cursor-pointer"
      type="button"
    ></button>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  top: string;
  left: string;
}>();
</script>

<style scoped></style>
