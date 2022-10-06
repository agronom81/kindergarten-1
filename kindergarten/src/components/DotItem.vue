<template>
  <div
    ref="root"
    class="absolute w-8 h-8 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="block w-52 h-26 bg-white shadow-2xl p-4 top-[-6rem] left-[-87px] rounded-md fade-in"
    >
      <div class="flex flex-col">
        <div class="block">
          <img :src="content.imgPath" :alt="content.label" />
        </div>
        <div class="block">
          <p class="mb-2">
            <strong>{{ content.label }}:</strong> {{ content.description }}
          </p>
        </div>
      </div>
    </div>
    <button
      @click="showPopUp"
      class="absolute top-[50%] left-[50%] translate-x-[-50%] hover:w-8 hover:h-8 transition-all translate-y-[-50%] w-6 h-6 bg-white cursor-pointer rounded-full"
      type="button"
    ></button>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import sound from "../assets/audio/onceagain.mp3";
defineProps<{
  top: string;
  left: string;
  content: {
    label: string;
    imgPath?: string;
    description: string;
  };
}>();

const root = ref<HTMLElement | null>(null);
const isShow = ref(false);
const audio = ref<HTMLAudioElement>();
const showPopUp = () => {
  if (!isShow.value) {
    playSound(sound);
  }
  isShow.value = !isShow.value;
};

const playSound = (sound: string) => {
  if (sound) {
    audio.value = new Audio(sound);
    audio.value?.play();
  }
};

const clickOutside = () => {
  const onClickOutside = (e: any) => {
    if (root.value) {
      if (!root.value?.contains(e.target)) {
        audio.value?.pause();
      }

      // audio.value?.currentTime = 0;
      isShow.value = root.value?.contains(e.target);
    }
  };
  document.addEventListener("click", onClickOutside);
  onBeforeUnmount(() => {
    document.removeEventListener("click", onClickOutside);
  });
};

onMounted(() => {
  clickOutside();
});
</script>

<style scoped>
.dotItem {
  top: 20px;
  left: 20px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
</style>
