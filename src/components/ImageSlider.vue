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
  require('@/assets/image/portfolio/portfolio-main-1.png'),
  require('@/assets/image/portfolio/portfolio-main-2.png'),
  require('@/assets/image/portfolio/portfolio-main-3.png'),
  require('@/assets/image/portfolio/portfolio-main-4.png')
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
  imageTimer = setInterval(imageSlideTimer, 3000);
});

onUnmounted(() => {
  clearInterval(imageTimer);
});
</script>

<style scoped>

/* WELCOME AREA */
.welcome-area {
  height: auto;
}

.welcome-area > .container {
  position: relative;
  height: 100%;
}

.welcome-area > .container > .image-slide {
  height: 100%;
}

.welcome-area > .container > .image-slide > img{
  object-fit: contain;
}

.welcome-area > .container > .image-prev,
.welcome-area > .container > .image-next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  padding: 16px;
  margin-top: -22px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

.welcome-area > .container > .image-next {
  right: 0;
  border-radius: 3px 0 0 3px;
}

.welcome-area > .container > .image-prev:hover,
.welcome-area > .container > .image-next:hover {
  background-color: rgba(0, 0, 0, 0.8);
}

.welcome-area > .container > .dots {
  position: absolute;
  width: 100%;
  bottom: 10px;
  text-align: center;
}

.welcome-area > .container > .dots > .dot {
  cursor: pointer;
  height: 4px;
  width: 30px;
  margin: 0 2px;
  background-color: #717171;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.welcome-area > .container > .dots > .dot.active,
.welcome-area > .container > .dots > .dot:hover {
  background-color: #ddd;
}

.welcome-area > .container > .fade {
  -webkit-animation-name: fade;
  -webkit-animation-duration: 1.5s;
  animation-name: fade;
  animation-duration: 1.5s;
}

@-webkit-keyframes fade {
  from {
    opacity: .4
  }
  to {
    opacity: 1
  }
}

@keyframes fade {
  from {
    opacity: .4
  }
  to {
    opacity: 1
  }
}

</style>