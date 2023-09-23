<script setup lang="ts">
import errorImage from '../assets/error.svg'; // Импортируйте изображения
import bagImage from '../assets/bag.svg';

const props = defineProps<{
  img: string,
  text: string,
  titleText: string,
  titleColor: {
    type: string,
    default: "#ffffff"
  },
  light: {
    type: string,
    default: "radial-gradient(circle, rgba(255, 0, 0, 0.75) 0%, rgba(255, 0, 0, 0.35) 25%, rgba(0,0,0,0) 60%)"
  }
}>();

// Функция, которая возвращает URL изображения в зависимости от переданного параметра img
function getImageUrl(imgType) {
  switch (imgType) {
    case "error":
      return errorImage;
    case "bag":
      return bagImage;
    default:
      return "";
  }
}

</script>

<template>
  <div class="container">
    <span class="light" :style="{ background: light }"></span>
    <img :src="getImageUrl(props.img)" style="width: 20px">
    <div class="main">
      <h2 :style="{ color: props.titleColor }">{{ props.titleText }}</h2>
      <div class="text">
        {{ props.text }}
      </div>
    </div>
  </div>
</template>

<style scoped>
  .container {
    position: relative;
  }
  .light {
    position: absolute;
    width: 100%;
    height: 140px;
    top: -90px;
    left: 50%;
    transform: translate(-50%, 0);
    z-index: 1;
  }
  .main h2 {
    font-size: 18px;
    font-weight: 700;
  }
  .text {
    font-size: 12px;

  }
  .container img,
  .container div {
    position: relative;
    z-index: 10;
  }
</style>
