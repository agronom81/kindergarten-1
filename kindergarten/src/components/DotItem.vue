<template>
  <div
    ref="root"
    class="absolute w-8 h-8 rounded-full dotItem border"
    :style="{ top: top, left: left }"
  >
    <div
      v-show="isShow"
      class="block w-52 h-24 bg-white shadow-2xl p-2 top-[-5rem] left-[-87px] rounded-md fade-in"
    >
      <p>
        <strong>{{ content.label }}:</strong> {{ content.description }}
      </p>
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
const showPopUp = () => {
  if (!isShow.value) {
    playSound("http://soundbible.com/mp3/Grouse-SoundBible.com-381035918.mp3");
  }
  isShow.value = !isShow.value;
};

const playSound = (sound: string) => {
  if (sound) {
    var audio = new Audio(sound);
    audio.play();
  }
};

const clickOutside = () => {
  const onClickOutside = (e: any) => {
    if (root.value) {
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
