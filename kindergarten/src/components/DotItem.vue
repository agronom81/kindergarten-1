<template>
  <div
    ref="root"
    class="absolute w-8 h-8 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="block w-52 h-26 bg-white shadow-2xl p-4 top-[-5rem] left-[-87px] rounded-md fade-in"
    >
      <div class="flex flex-col">
        <p class="mb-2 flex-grow">
          <strong>{{ content.label }}:</strong> {{ content.description }}
        </p>
        <button type="button" @click="soundStop" v-if="audioPlay">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-8 h-8 pointer-events-none"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M14.25 9v6m-4.5 0V9M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
        </button>
        <button type="button" @click="soundStart" v-if="!audioPlay">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-8 h-8 pointer-events-none"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
            />
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M15.91 11.672a.375.375 0 010 .656l-5.603 3.113a.375.375 0 01-.557-.328V8.887c0-.286.307-.466.557-.327l5.603 3.112z"
            />
          </svg>
        </button>
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
    url?: string;
    description: string;
  };
}>();

const root = ref<HTMLElement | null>(null);
const isShow = ref(false);
const audio = ref<HTMLAudioElement>();
const audioPlay = ref(false);
const showPopUp = () => {
  if (!isShow.value) {
    playSound(sound);
  }
  isShow.value = !isShow.value;
};

const playSound = (sound: string) => {
  if (sound) {
    audio.value = new Audio(sound);
    soundStart();
  }
};

const soundStop = () => {
  audio.value?.pause();
  audioPlay.value = false;
};

const soundStart = () => {
  audio.value?.play();
  audioPlay.value = true;
};

const clickOutside = () => {
  const onClickOutside = (e: any) => {
    if (root.value) {
      if (!root.value?.contains(e.target)) {
        audio.value?.pause();
        audioPlay.value = false;
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
