<template>
  <header :class="{ 'header-area': true, 'navbar-fixed': isNavbarFixed, 'navbar-fade': true }" id="header">
    <nav class="navbar">
      <a class="navbar-brand" @click="moveTo('brand')">logo</a>
      <a class="navbar-toggler" @click="menuToggle"><i class="fa fa-bars"></i></a>
      <div class="navbar-menu" :class="{ show: isMenuVisible }" id="menu">
        <div class="nav-item"><a class="nav-link" @click="moveTo('about')">about</a></div>
        <div class="nav-item"><a class="nav-link" @click="moveTo('career')">career</a></div>
        <div class="nav-item"><a class="nav-link" @click="moveTo('portfolio')">portfolio</a></div>
        <div class="nav-item"><a class="nav-link" @click="moveTo('service')">service</a></div>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const isNavbarFixed = ref(false);
const isMenuVisible = ref(false);

const handleScroll = () => {
  isNavbarFixed.value = document.documentElement.scrollTop > 70;
};

const menuToggle = () => {
  isMenuVisible.value = !isMenuVisible.value;
};

const moveTo = (id) => {
  if (id === 'brand') {
    window.scrollTo(0, 0);
  } else {
    const element = document.getElementById(id);
    if (element) {
      window.scrollTo(0, element.offsetTop - 70);
    }
  }
  isMenuVisible.value = false; // 메뉴 닫기
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});
</script>

<style scoped>
/* 스타일 추가 */
</style>
