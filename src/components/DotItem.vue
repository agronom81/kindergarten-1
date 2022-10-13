<template>
  <div
    ref="root"
    class="absolute w-8 h-8 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="flex justify-center items-center h-52 bg-white shadow-2xl p-4 top-[-12rem] left-[-87px] rounded-md fade-in w-52"
    >
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
