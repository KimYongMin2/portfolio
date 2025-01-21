<template>
  <section class="career-area" id="career">
    <div class="title">CAREER</div>
    <div class="container">
      <div class="item" v-for="(career, index) in careers" :key="index">
        <div class="icon">
          <span><i :class="career.icon"></i></span>
        </div>
        <div class="service">{{ career.name }}</div>
        <div class="content">{{ career.detail }}</div>
        <div class="content">{{ career.description }}</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

// 서비스 정보 배열 설정
const careers = ref([
  {
    name: '명지전문대',
    icon: 'fa-solid fa-school',
    detail: '컴퓨터전자과(3년제) 2015.02 - 2020.02',
    description: '웹페이지 만들기, Java, C 등 기본적인 프로그래밍 언어를 학습했습니다.'
  },
  {
    name: '명지전문대',
    icon: 'fa-solid fa-school',
    detail: '전자공학과(학사학위과정) 2020.02 - 2021.02',
    description: '데이터통신 및 알고리즘 언어를 학습햇습니다.'
  },
  {
    name: '비트캠프',
    icon: 'fa-solid fa-school',
    detail: '디지털컨버전스 기반 Framework 전문 개발자 양성과정 2021.04 - 2021.10',
    description: 'Java, Database, Javascript, AWS 등 기본적인 내용을 학습하였습니다.'
  },
  {
    name: '소프트브리지',
    icon: 'fa-solid fa-building',
    detail: '개발2팀 2022.02 -',
    description: 'Java, Javascript를 사용한 화상회의 웹 플랫폼 및 Vue를 사용한 management 플랫폼을 만드는 프로젝트를 작업하였습니다.'
  }
]);
</script>

<style scoped>
/* 여기에 필요한 스타일을 추가하세요 */
</style>
