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

/* HEADER */
.header-area {
  position: relative;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 99;
  background-color: white;
  border-bottom: 1px solid #d5d5d5;
}

.navbar-fade {
  animation-name: navbar-fade;
  animation-duration: 0.5s;
  -webkit-animation-name: navbar-fade;
  -webkit-animation-duration: 0.5s;
}

@keyframes navbar-fade {
  from {
    opacity: .4
  }
  to {
    opacity: 1
  }
}

@-webkit-keyframes navbar-fade {
  from {
    opacity: .4
  }
  to {
    opacity: 1
  }
}

.header-area.navbar-fixed {
  position: fixed;
}

.header-area > .navbar {
  width: calc(100% - 120px);
  margin: 0 60px;
  overflow: hidden;
}

@media (min-width: 992px) {
  .header-area > .navbar {
    max-width: 900px;
    margin: 0 auto;
  }
}

@media (min-width: 1200px) {
  .header-area > .navbar {
    max-width: 1000px;
  }
}

.header-area > .navbar > .navbar-brand {
  display: inline-block;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 32px;
  cursor: pointer;
}

.header-area > .navbar > .navbar-toggler * {
  font-size: 32px;
}

.header-area > .navbar > .navbar-toggler {
  float: right;
  height: 70px;
  line-height: 70px;
  font-size: 32px;
  cursor: pointer;
}

@media (min-width: 992px) {
  .header-area > .navbar > .navbar-toggler {
    display: none;
  }
}

.header-area > .navbar > .navbar-menu {
  position: absolute;
  background-color: rgba(0, 0, 0, 0.5);
  top: 70px;
  left: 0;
  width: 100%;
  height: 0;
  transition: 0.5s ease;
  overflow: hidden;
}

.header-area > .navbar > .navbar-menu.show {
  height: 200px;
}

.header-area > .navbar > .navbar-menu > .nav-item {
  float: none;
  display: block;
  height: 50px;
  line-height: 50px;
}

.header-area > .navbar > .navbar-menu > .nav-item:hover * {
  background-color: rgba(0, 0, 0, 0.4);
}

.header-area > .navbar > .navbar-menu > .nav-item > .nav-link {
  display: block;
  padding-left: 50px;
  color: white;
  cursor: pointer;
  font-family: "Montserrat";
}

@media (min-width: 992px) {
  .header-area > .navbar > .navbar-menu {
    position: relative;
    background-color: transparent;
    float: right;
    top: 0;
    width: auto;
    height: auto;
    transition: none;
  }

  .header-area > .navbar > .navbar-menu.show {
    height: auto;
  }

  .header-area > .navbar > .navbar-menu > .nav-item {
    display: inline-block;
    height: 70px;
    line-height: 70px;
  }

  .header-area > .navbar > .navbar-menu > .nav-item:hover * {
    background-color: transparent;
  }

  .header-area > .navbar > .navbar-menu > .nav-item > .nav-link {
    display: block;
    padding: 0 20px;
    color: black;
  }
}

</style>
