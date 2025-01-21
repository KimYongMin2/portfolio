<template>
  <section class="portfolio-area" id="portfolio">
    <div class="title">PORTFOLIO</div>
    <div class="filter">
      <ul class="list">
        <li class="listItem" :class="{'active': currentFilter === 'all'}" @click="filterSelection('all')">All</li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentFilter === 'company'}" @click="filterSelection('company')">COMPANY</li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentFilter === 'study'}" @click="filterSelection('study')">STUDY</li>
      </ul>
    </div>
    <div class="container">
      <div class="filterItem show" v-for="(item, index) in filteredPortfolioItems" :key="index" :class="item.filters">
        <div class="image" @click="viewPortfolio(item)">
          <div class="overlay"><i class="fa-solid fa-magnifying-glass"></i></div>
          <img :src="item.image">
        </div>
        <div class="main">{{ item.title }}</div>
        <div class="sub">{{ item.subtitle }}</div>
        <div class="text">{{ item.description }}</div>
      </div>
    </div>

    <div id="portfolioModal" class="modal" v-if="isModalOpen">
      <span class="close" @click="closeModal">&times;</span>
      <div class="container">
        <img :src="modalData.image" id="modalImage">
        <div id="modalMain" class="modal-main">{{ modalData.main }}</div>
        <div id="modalSub" class="modal-sub">{{ modalData.sub }}</div>
        <div id="modalText" class="modal-text">{{ modalData.text }}</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';

const currentFilter = ref('all');
const isModalOpen = ref(false);
const modalData = ref({
  image: '',
  main: '',
  sub: '',
  text: ''
});

const portfolioItems = ref([
  { title: '에듀몬스터', subtitle: '온라인 강의 플랫폼', description: '포트 폴리오 상세 설명', image: require('@/assets/image/edumonster/edu-logo.png'), filters: 'company' },
  { title: 'Meet U', subtitle: '비대면 라이프 서비스 플랫폼', description: '포트 폴리오 상세 설명', image: require('@/assets/image/lg-meet/lg-meet-logo.png'), filters: 'company' },
  { title: 'MATE', subtitle: '화상회의 서비스 플랫폼', description: '포트 폴리오 상세 설명', image: require('@/assets/image/mate/mate-logo.png'), filters: 'company' },
  { title: '리만 LMS', subtitle: 'Learning Management System', description: '포트 폴리오 상세 설명', image: require('@/assets/image/riman-lms/riman-lms-logo.png'), filters: 'company' },
  { title: '리만 BO', subtitle: '리만 글로벌 전환 신규 플랫폼', description: '포트 폴리오 상세 설명', image: require('@/assets/image/riman-lms/riman-bo-logo.png'), filters: 'company' },
  { title: '책꽂이', subtitle: '도서 관리 프로그램', description: '초기 미니프로젝트인 만큼 Java에 대한 기본지식과 프로젝트의 전체적인 진행과정을 알 수 있었으며 JDBC기능 및 OOP의 이해, 리펙토링을 통한 더 나은 코드가 무엇인 지 탐구할 수 있었습니다.', image: require('@/assets/image/practice-project/practice-project-bookclip.png'), filters: 'study' },
  { title: '오를래', subtitle: '산 정보 및 SNS 프로그램', description: '학원 팀 프로젝트로 웹사이트 개발에 따른 JavaScript, Database, Java를 사용하였으며 AWS(인스턴스)를 사용한 배포, MVC패턴 이해, 다양한 API 사용을 통한 스킬강화를 할 수 있었습니다.', image: require('@/assets/image/practice-project/mountain-main-logo.png'), filters: 'study' },
  { title: '계산기', subtitle: '간단한 계산 프로그램', description: '미니 서브프로젝트로 Java를 이용한 다양한 수식을 할 수 있게 프로그래밍을 짰으며 사용자의 편의를 생각하며 좀 더 직관적이고 사용하기 편하게 추가 개발하였습니다.', image: require('@/assets/image/practice-project/cal-logo.png'), filters: 'study' },
]);

const filteredPortfolioItems = computed(() => {
  if (currentFilter.value === 'all') return portfolioItems.value;
  return portfolioItems.value.filter(item => item.filters.includes(currentFilter.value));
});

function filterSelection(filter) {
  currentFilter.value = filter;
}

function viewPortfolio(item) {
  modalData.value = {
    image: item.image,
    main: item.title,
    sub: item.subtitle,
    text: item.description
  };
  isModalOpen.value = true;
}

function closeModal() {
  isModalOpen.value = false;
}
</script>

<style scoped>
/* 여기에 필요한 CSS 스타일 추가 */
</style>
