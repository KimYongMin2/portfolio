<template>
  <section class="portfolio-area" id="portfolio">
    <div class="title">PORTFOLIO</div>
    <div class="filter">
      <ul class="list">
        <li class="listItem" :class="{'active': currentFilter === 'all'}" @click="filterSelection('all')">All</li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentFilter === 'company'}" @click="filterSelection('company')">
          COMPANY
        </li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentFilter === 'study'}" @click="filterSelection('study')">STUDY</li>
      </ul>
    </div>
    <div class="container">
      <div class="filterItem show" v-for="(item, index) in filteredPortfolioItems" :key="index" :class="item.filters">
        <div class="image">
          <div class="overlay"><i class="fa-solid fa-magnifying-glass"></i></div>
          <img :src="item.image">
        </div>
        <div class="main">{{ item.title }}</div>
        <div class="sub">{{ item.subtitle }}</div>
        <div class="text">{{ item.description }}</div>
      </div>
    </div>
  </section>
</template>

<script setup>
import {ref, computed} from 'vue';

const currentFilter = ref('all');

const portfolioItems = ref([
  {
    title: '에듀몬스터',
    subtitle: '온라인 강의 플랫폼',
    description: '온라인 강의를 판매하는 플랫폼으로 각 강의들을 소개하는페이지, 공지사항, 이벤트 등 쇼핑몰의 형태로 구성이 되어있습니다. 기술스택으로는  Vue, Javascript, Html, Css를 사용하였습니다.',
    image: require('@/assets/image/edumonster/edu-logo.png'),
    imageDetail: [require('@/assets/image/edumonster/edu-class.png'), require('@/assets/image/edumonster/edu-class-detail.png'), require('@/assets/image/edumonster/edu-main.png')],
    filters: 'company'
  },
  {
    title: 'Meet U',
    subtitle: '비대면 라이프 서비스 플랫폼',
    description: '사용자가 만들거나 참여할 수 있는 회의방을 보여주고 화상회의를 할 수 있는 플랫폼으로 WebRTC를 기반으로 하여 Zoom과 유사한 다양한 기능 및 실시간 화상회의 기능을 제공합니다.' +
        '이 플랫폼은 사용자가 원하는 방식으로 회의 방을 탐색할 수 있도록 카드, 리스트, 캘린더 형식으로 다양한 UI를 제공하고 WebRTC를 통해 화상 통화와 데이터 전송을 지원합니다.' +
        '또한 화면공유, 파일공유, 실시간 채팅, 그림판 등 참가자 간의 원활한 협업을 지원하며 회의록 기능 및 녹화 기능도 제공합니다. ' +
        '기술 스택으로는 Java, JavaScript, HTML, CSS를 사용하였습니다.',
    image: require('@/assets/image/lg-meet/lg-meet-logo.png'),
    imageDetail: [require('@/assets/image/lg-meet/lg-meet-logo.png')],
    filters: 'company'
  },
  {
    title: 'MATE',
    subtitle: '화상회의 서비스 플랫폼',
    description: '사용자가 만들거나 참여할 수 있는 회의방을 보여주고 화상회의를 할 수 있는 플랫폼으로 WebRTC를 기반으로 하여 Zoom과 유사한 다양한 기능 및 실시간 화상회의 기능을 제공합니다.' +
        '이 플랫폼은 사용자가 원하는 방식으로 회의 방을 탐색할 수 있도록 카드, 리스트, 캘린더 형식으로 다양한 UI를 제공하고 WebRTC를 통해 화상 통화와 데이터 전송을 지원합니다.' +
        '또한 화면공유, 파일공유, 실시간 채팅, 그림판 등 참가자 간의 원활한 협업을 지원하며 회의록 기능 및 녹화 기능도 제공합니다. ' +
        '기술 스택으로는 Java, JavaScript, HTML, CSS를 사용하였습니다.',
    image: require('@/assets/image/mate/mate-logo.png'),
    imageDetail: [require('@/assets/image/mate/mate-logo.png')],
    filters: 'company'
  },
  {
    title: '리만 LMS',
    subtitle: 'Learning Management System',
    description: '회원에게 온라인 강의를 보여주는 플랫폼으로 각 강의들을 소개하는페이지, 장바구니 및 유,무료 강의들을 보여주는 페이지 등으로 나누어져 있습니다.' +
        '관리자 페이지는 강의들 및 강의들의 교육자료를 등록 가능하고 강의마다 댓글 및 문의사항 기능도 구현하였습니다. 기술스택으로는  Vue, Javascript, Html, Css를 사용하였습니다.',
    image: require('@/assets/image/riman-lms/riman-lms-logo.png'),
    imageDetail: [require('@/assets/image/riman-lms/riman-lms-logo.png')],
    filters: 'company'
  },
  {
    title: '리만 BO',
    subtitle: '리만 글로벌 전환 신규 플랫폼',
    description: '이 플랫폼은 전반적인 사용자 관리 및 웹페이지 관리를 할 수 있는 플랫폼으로 메인페이지의 약관, 다양한 쿠폰, 메인광고이미지 및 동영상 등을 관리하며 사용자는 사용자의 정보, 권한을 관리합니다.' +
        '기술스텍으로는 JavaScript, Vue, Html, Css를 사용합니다',
    image: require('@/assets/image/riman-lms/riman-bo-logo.png'),
    imageDetail: [require('@/assets/image/riman-lms/riman-bo-logo.png')],
    filters: 'company'
  },
  {
    title: '오를래',
    subtitle: '산 정보 및 SNS 프로그램',
    description: '오를래는 학원 팀 프로젝트로 산에 대한 정보(위치, 높이, 특색)등을 제공하며 각 사용자들이 자유롭게 이용 가능한 자유게시판을 SNS 형식으로 제작하였습니다. ' +
        '사용자들은 크루활동도 가능하며 크루모집, 크루원 관리 등을 할 수 있습니다. 또한 관리자 페이지도 따로 만들어 올바른 정보가 유지 될 수 있도록 하였으며 관리자 페이지에서' +
        '게시물들을 관리 할 수 있습니다. 웹사이트 개발에 따른 JavaScript, Database, Java를 사용하였으며 AWS(인스턴스)를 사용한 배포, MVC패턴 이해, 다양한 API 사용을 통한 스킬강화를 할 수 있었습니다.',
    image: require('@/assets/image/practice-project/mountain-main-logo.png'),
    imageDetail: [require('@/assets/image/practice-project/mountain-main-logo.png')],
    filters: 'study'
  },
  {
    title: '책꽂이',
    subtitle: '도서 관리 프로그램',
    description: '이 프로그램은 미니 프로젝트로 DataBase에 책을 넣고, 빌리고, 반납하는 등의 기능을 만들어 사용자 및 관리자가 도서를 효율적으로 관리 및 대여 할 수 있도록 제작하였습니다.' +
        '초기 미니프로젝트인 만큼 Java에 대한 기본지식과 프로젝트의 전체적인 진행과정을 알 수 있었으며 JDBC기능 및 OOP의 이해, 리펙토링을 통한 더 나은 코드가 무엇인 지 탐구할 수 있었습니다.' +
        '기술 스택으로는 Java를 사용하였습니다. ',
    image: require('@/assets/image/practice-project/practice-project-bookclip.png'),
    imageDetail: [require('@/assets/image/practice-project/practice-project-bookclip.png')],
    filters: 'study'
  },
  {
    title: '계산기',
    subtitle: '간단한 계산 프로그램',
    description: '미니 서브프로젝트로 Java를 이용하여 사용자의 입력을 통해 다양한 수식을 짤 수 있게 프로그래밍을 했으며 사용자의 편의를 생각하며 좀 더 직관적이고 사용하기 편하게 추가 개발하였습니다.',
    image: require('@/assets/image/practice-project/cal-logo.png'),
    imageDetail: [require('@/assets/image/practice-project/cal-logo.png')],
    filters: 'study'
  },
]);

const filteredPortfolioItems = computed(() => {
  if (currentFilter.value === 'all') return portfolioItems.value;
  return portfolioItems.value.filter(item => item.filters.includes(currentFilter.value));
});

function filterSelection(filter) {
  currentFilter.value = filter;
}

</script>

<style scoped>
/* 여기에 필요한 CSS 스타일 추가 */
</style>
