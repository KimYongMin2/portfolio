<template>
  <div class="section-container">
    <div class="welcome-area">
      <div class="container">
        <div class="image-slide fade" v-for="(image, index) in images" :key="index" v-show="currentImageIndex === index">
          <img :src="image" alt="슬라이드 이미지">
        </div>

        <a class="image-prev" id="imagePrev" @click="plusImageSlides(-1)">&#10094;</a>
        <a class="image-next" id="imageNext" @click="plusImageSlides(1)">&#10095;</a>

        <div class="dots">
          <span class="dot" v-for="(image, index) in images" :key="index" @click="currentImageSlide(index)" :class="{ active: currentImageIndex === index }"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const images = ref([
  require('@/assets/image/edumonster/edu-main.png'),
  require('@/assets/image/lg-meet/lg-meet-main.png'),
  require('@/assets/image/practice-project/practice-project-bookclip.png'),
  require('@/assets/image/riman-lms/riman-lms-main.png')
]);

const currentImageIndex = ref(0);
let imageTimer = null;

const showImageSlides = (index) => {
  currentImageIndex.value = index < 0 ? images.value.length - 1 : index % images.value.length;
};

const imageSlideTimer = () => {
  showImageSlides(currentImageIndex.value + 1);
};

const plusImageSlides = (n) => {
  clearInterval(imageTimer);
  showImageSlides(currentImageIndex.value + n);
  imageTimer = setInterval(imageSlideTimer, 3000);
};

const currentImageSlide = (n) => {
  clearInterval(imageTimer);
  showImageSlides(n);
  imageTimer = setInterval(imageSlideTimer, 3000);
};

onMounted(() => {
  // imageTimer = setInterval(imageSlideTimer, 3000);
});

onUnmounted(() => {
  // clearInterval(imageTimer);
});
</script>

<style scoped>

</style>