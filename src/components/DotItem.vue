<template>
  <div
    ref="root"
    class="absolute w-10 h-10 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="flex justify-center items-center h-52 bg-white shadow-2xl p-4 top-[-12rem] left-[-87px] rounded-md fade-in w-52"
    >
      <button class="close-btn" @click="closePopup">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-8 h-8"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </button>
      <img
        class="block w-full rounded-md"
        :src="content.imgPath"
        :alt="content.label"
      />
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
// import sound from "../assets/audio/onceagain.mp3";
const props = defineProps<{
  top: string;
  left: string;
  content: {
    label: string;
    imgPath?: string;
    sound: any;
  };
}>();

const root = ref<HTMLElement | null>(null);
const isShow = ref(false);
const audio = ref<HTMLAudioElement>();
const showPopUp = () => {
  if (!isShow.value) {
    playSound(props.content.sound);
  }
  isShow.value = !isShow.value;
};

const playSound = (sound: string) => {
  if (sound) {
    audio.value = new Audio(sound);
    audio.value?.play();
  }
};

const closePopup = () => {
  if (audio.value) {
    audio.value?.pause();
  }
  isShow.value = !isShow.value;
};

const clickOutside = () => {
  const onClickOutside = (e: any) => {
    if (root.value) {
      if (!root.value?.contains(e.target)) {
        audio.value?.pause();
        isShow.value = false;
      }
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
