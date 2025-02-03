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
      <div class="filterItem show" v-for="(item, index) in filteredPortfolioItems" :key="index" :class="item.filters"
           @click="setModalInfo(item)">
        <div class="image">
          <div class="overlay"><i class="fa-solid fa-magnifying-glass"></i></div>
          <img :src="item.image">
        </div>
        <div class="main">{{ item.title }}</div>
        <div class="sub">{{ item.subtitle }}</div>
        <div class="text">{{ item.description }}</div>
      </div>
    </div>
    <div class="modal" v-if="modalState">
      <span class="close" id="modalClose" @click="closeModal">&times;</span>
      <div class="picture fade" v-for="(image, index) in modalInfo.imageDetail" :key="index" v-show="currentImageIndex === index">
        <img :src="image" alt="슬라이드 이미지">
        <a class="image-prev" id="imagePrev" @click="plusImageSlides(-1)">&#10094;</a>
        <a class="image-next" id="imageNext" @click="plusImageSlides(1)">&#10095;</a>

        <div class="dots">
          <span class="dot" v-for="(image, index) in modalInfo.imageDetail" :key="index" @click="currentImageSlide(index)" :class="{ active: currentImageIndex === index }"></span>
        </div>
      </div>
      <div class="text">
        <div class="intro">
          {{ modalInfo.description }}
          <br>
        </div>
        <ul>
          <li>
            <div class="info">
              <i class="fa-solid fa-screwdriver-wrench"></i> <div>{{ modalInfo.tool }}</div>
            </div>
          </li>
          <li>
            <div class="info">
              <i class="fa-regular fa-rectangle-list"></i> <div><div style="margin-bottom: 5px" v-for="(item) in modalInfo.assignedTask" :key="item">{{ item }}</div></div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <div class="modal-overlay" v-if="modalState">
    </div>
  </section>
</template>

<script setup>
import {ref, computed} from 'vue';
const currentImageIndex = ref(0);

const currentFilter = ref('all');
const modalInfo = ref();
const modalState = ref(false)
const portfolioItems = ref([
  {
    title: '에듀몬스터',
    subtitle: '온라인 강의 플랫폼',
    description: '온라인 강의를 판매하는 플랫폼으로 각 강의들을 소개하는페이지, 공지사항, 이벤트 등 쇼핑몰의 형태로 구성이 되어있습니다.',
    tool: 'Vue, JavaScript, Html, Css',
    assignedTask: ['상품 리스트 및 상세정보 표출 페이지', '이용후기 및 문의사항 등록,수정,삭제 관리 페이지', '로그인,회원가입 및 구매 페이지', '회원, 컨텐츠 관리 페이지', '찜하기 및 장바구니 기능구현'],
    image: require('@/assets/image/edumonster/edu-logo.png'),
    imageDetail: [require('@/assets/image/edumonster/edu-main.png'), require('@/assets/image/edumonster/edu-class.png'),require('@/assets/image/edumonster/edu-class-detail.png')],
    filters: 'company'
  },
  {
    title: 'Meet U',
    subtitle: '비대면 라이프 서비스 플랫폼',
    description: '사용자가 만들거나 참여할 수 있는 회의방을 보여주고 화상회의를 할 수 있는 플랫폼으로 WebRTC를 기반으로 하여 Zoom과 유사한 다양한 기능 및 실시간 화상회의 기능을 제공합니다.' +
        '이 플랫폼은 사용자가 원하는 방식으로 회의 방을 탐색할 수 있도록 카드, 리스트, 캘린더 형식으로 다양한 UI를 제공하고 WebRTC를 통해 화상 통화와 데이터 전송을 지원합니다.' +
        '또한 화면공유, 파일공유, 실시간 채팅, 그림판 등 참가자 간의 원활한 협업을 지원하며 회의록 기능 및 녹화 기능도 제공합니다. ',
    tool: 'JavaScript, Html, Css, Java',
    assignedTask: ['회의 리스트 표출 페이지', '화면공유 기능', '발화자 하이라이트 기능'],
    image: require('@/assets/image/lg-meet/lg-meet-logo.png'),
    imageDetail: [require('@/assets/image/lg-meet/lg-meet-home.png'),require('@/assets/image/lg-meet/lg-meet-main.png'),require('@/assets/image/lg-meet/lg-meet-meeting.png')],
    filters: 'company'
  },
  {
    title: 'MATE',
    subtitle: '화상회의 서비스 플랫폼',
    description: '사용자가 만들거나 참여할 수 있는 회의방을 보여주고 화상회의를 할 수 있는 플랫폼으로 WebRTC를 기반으로 하여 Zoom과 유사한 다양한 기능 및 실시간 화상회의 기능을 제공합니다.' +
        '이 플랫폼은 사용자가 원하는 방식으로 회의 방을 탐색할 수 있도록 카드, 리스트, 캘린더 형식으로 다양한 UI를 제공하고 WebRTC를 통해 화상 통화와 데이터 전송을 지원합니다.' +
        '또한 화면공유, 파일공유, 실시간 채팅, 그림판 등 참가자 간의 원활한 협업을 지원하며 회의록 기능 및 녹화 기능도 제공합니다. ',
    tool: 'JavaScript, Html, Css, Java',
    assignedTask: ['회의 리스트 표출 페이지', '화면공유 기능', '영상송출 기능', '채팅기능', '그림판 기능', '입,퇴장 시 회의, 채팅 연결 기능'],
    image: require('@/assets/image/mate/mate-logo.png'),
    imageDetail: [require('@/assets/image/mate/mate-home.png'),require('@/assets/image/mate/mate-home2.png'),require('@/assets/image/mate/mate-main.png')],
    filters: 'company'
  },
  {
    title: '리만 LMS',
    subtitle: 'Learning Management System',
    description: '회원에게 온라인 강의를 보여주는 플랫폼으로 각 강의들을 소개하는페이지, 장바구니 및 유,무료 강의들을 보여주는 페이지 등으로 나누어져 있습니다.' +
        '관리자 페이지는 강의들 및 강의들의 교육자료를 등록 가능하고 강의마다 댓글 및 문의사항 기능도 구현하였습니다.',
    tool: 'Vue, JavaScript, Html, Css',
    assignedTask: ['상품 리스트 및 상세정보 표출 페이지', '이용후기 및 문의사항 등록,수정,삭제 관리 페이지', '로그인,회원가입 및 구매 페이지', '회원, 컨텐츠 관리 페이지', '찜하기 및 장바구니 기능구현'],
    image: require('@/assets/image/riman-lms/riman-lms-logo.png'),
    imageDetail: [require('@/assets/image/riman-lms/riman-lms-class.png'),require('@/assets/image/riman-lms/riman-lms-main.png'),require('@/assets/image/riman-lms/riman-lms-management.png'),require('@/assets/image/riman-lms/riman-lms-study.png')],
    filters: 'company'
  },
  {
    title: '리만 BO',
    subtitle: '리만 글로벌 전환 신규 플랫폼',
    description: '이 플랫폼은 전반적인 사용자 관리 및 웹페이지 관리를 할 수 있는 플랫폼으로 메인페이지의 약관, 다양한 쿠폰, 메인광고이미지 및 동영상 등을 관리하며 사용자는 사용자의 정보, 권한을 관리합니다.',
    tool: 'Vue, JavaScript, Html, Css',
    assignedTask: ['메뉴구성 페이지, 쿠폰정책 페이지', '주문 및 반품관리 페이지', '찾아오시는 길 페이지', '약관 페이지', '장바구니 관리 페이지', '... etc'],
    image: require('@/assets/image/riman-bo/riman-bo-logo.png'),
    imageDetail: [require('@/assets/image/riman-bo/riman-bo-main.png'),require('@/assets/image/riman-bo/riman-bo-map.png'),require('@/assets/image/riman-bo/riman-bo-menu.png')],
    filters: 'company'
  },
  {
    title: '오를래',
    subtitle: '산 정보 및 SNS 프로그램',
    description: '오를래는 학원 팀 프로젝트로 산에 대한 정보(위치, 높이, 특색)등을 제공하며 각 사용자들이 자유롭게 이용 가능한 자유게시판을 SNS 형식으로 제작하였습니다. ' +
        '사용자들은 크루활동도 가능하며 크루모집, 크루원 관리 등을 할 수 있습니다. 또한 관리자 페이지도 따로 만들어 올바른 정보가 유지 될 수 있도록 하였으며 관리자 페이지에서' +
        '게시물들을 관리 할 수 있습니다. 웹사이트 개발에 따른 JavaScript, Database, Java를 사용하였으며 AWS(인스턴스)를 사용한 배포, MVC패턴 이해, 다양한 API 사용을 통한 스킬강화를 할 수 있었습니다.',
    tool: 'JavaScript, Html, Css, Java',
    assignedTask: ['산 정보조회 api 기능', '산 리스트 및 상세정보 보여주는 페이지', '산과 관련된 SNS를 필터링 해 보여주는 기능', '관리자 페이지'],
    image: require('@/assets/image/practice-project/mountain-main-logo.png'),
    imageDetail: [require('@/assets/image/practice-project/mountain_main.png'),require('@/assets/image/practice-project/mountain-sns.png'),require('@/assets/image/practice-project/mountain-info.png'),require('@/assets/image/practice-project/mountain-crew.png'),require('@/assets/image/practice-project/mountain-management.png')],
    filters: 'study'
  },
  {
    title: '책꽂이',
    subtitle: '도서 관리 프로그램',
    description: '이 프로그램은 미니 프로젝트로 DataBase에 책을 넣고, 빌리고, 반납하는 등의 기능을 만들어 사용자 및 관리자가 도서를 효율적으로 관리 및 대여 할 수 있도록 제작하였습니다.' +
        '초기 미니프로젝트인 만큼 Java에 대한 기본지식과 프로젝트의 전체적인 진행과정을 알 수 있었으며 JDBC기능 및 OOP의 이해, 리펙토링을 통한 더 나은 코드가 무엇인 지 탐구할 수 있었습니다.' +
        '기술 스택으로는 Java를 사용하였습니다. ',
    tool: 'Java',
    assignedTask: ['사용자의 입력을 받아 도서 대여, 반납, 추가하는 기능'],
    image: require('@/assets/image/practice-project/practice-project-bookclip.png'),
    imageDetail: [require('@/assets/image/practice-project/practice-project-bookclip.png')],
    filters: 'study'
  },
  {
    title: '계산기',
    subtitle: '간단한 계산 프로그램',
    description: '미니 서브프로젝트로 Java를 이용하여 사용자의 입력을 통해 다양한 수식을 짤 수 있게 프로그래밍을 했으며 사용자의 편의를 생각하며 좀 더 직관적이고 사용하기 편하게 추가 개발하였습니다.',
    tool: 'Java',
    assignedTask: ['사용자의 입력을 받아 계산하는 기능'],
    image: require('@/assets/image/practice-project/cal-logo.png'),
    imageDetail: [require('@/assets/image/practice-project/cal-logo.png')],
    filters: 'study'
  },
]);

function setModalInfo(portFolioInfo) {
  currentImageIndex.value = 0
  modalInfo.value = portFolioInfo;
  modalState.value = true;
}

function closeModal() {
  modalInfo.value = null;
  modalState.value = false;
}

const plusImageSlides = (n) => {
  showImageSlides(currentImageIndex.value + n);
};

const showImageSlides = (index) => {
  currentImageIndex.value = index < 0 ? modalInfo.value.imageDetail.length - 1 : index % modalInfo.value.imageDetail.length;
};

const currentImageSlide = (n) => {
  showImageSlides(n);
};

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
/* PORTFOLIO AREA */
.portfolio-area {
  height: auto;
}

.portfolio-area > .filter > .list {
  text-align: center;
}

.portfolio-area > .filter > .list > .listItem {
  display: inline-block;
  font-weight: bold;
  /*padding: 0 20px;*/
  font-size: 16px;
  cursor: pointer;
  /*border-bottom: 1px solid #d5d5d5;*/
  font-family: "Montserrat";
}

.portfolio-area > .filter > .list > .listItemSlash {
  display: inline-block;
  font-weight: bold;
  padding: 0 20px;
  font-size: 16px;
  color: #717171;
}

.portfolio-area > .filter > .list > .listItem:hover,
.portfolio-area > .filter > .list > .listItem.active {
  color: royalblue;
}

.portfolio-area > .container {
  display: flex;
  flex-wrap: wrap; /* 여러 줄로 배치 가능 */
  justify-content: center; /* 수평 가운데 정렬 */
  max-width: 1200px; /* 최대 너비 설정 (선택 사항) */
  width: 100%; /* 전체 너비 사용 */
}

.portfolio-area > .container > .filterItem {
  display: none;
  width: calc(60% - 80px);
  margin: 24px;
  text-align: center;
  padding: 10px;
  /*border: 1px solid #d5d5d5;*/
  /*border-radius: 50px;*/
}

@media (min-width: 800px) {
  .portfolio-area > .container > .filterItem {
    width: calc(30% - 80px);
  }
}

@media (min-width: 992px) {
  .portfolio-area > .container > .filterItem {
    width: calc(25% - 80px);
  }
}

.portfolio-area > .container > .filterItem.show {
  display: inline-block;

}

.portfolio-area > .container > .filterItem > .image {
  position: relative;
  max-height: 150px;
  display: flex;
  justify-content: center;
}

@media (min-width: 992px) {
  .portfolio-area > .container > .filterItem > .image {
    height: 150px;
    display: flex;
    justify-content: center;
  }
}

.portfolio-area > .container > .filterItem > .image > .overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: all 300ms ease;
  /*border-radius: 50px;*/
  cursor: pointer;
}

.portfolio-area > .container > .filterItem > .image:hover > .overlay {
  background-image: linear-gradient(to right, #464545, #090000);
  opacity: 0.9;
}

.portfolio-area > .container > .filterItem > .image > .overlay > i {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 48px;
}

.portfolio-area > .container > .filterItem > .image > img {
  border-radius: 5px;
  object-fit: contain;
  height: auto;
  min-height: 150px;
}

.portfolio-area > .container > .filterItem > .main {
  font-size: 24px;
  font-weight: bold;
  padding: 10px 0;
  font-family: 'Pretendard-Regular';
  letter-spacing: -0.5px;
}

.portfolio-area > .container > .filterItem > .sub {
  font-size: 16px;
  color: #777;
  font-family: 'Pretendard-Regular';
  letter-spacing: -0.5px;
}

.portfolio-area > .container > .filterItem > .text {
  display: none;
}

.modal {
  display: flex;
  position: fixed;
  top: calc(50% + 50px);
  left: 50%;
  transform: translate(-50%, -50%);
  width: calc(50% + 50px);
  height: auto;
  min-height: 650px;
  background: white;
  border-radius: 15px;
  z-index: 3;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: center;
}

.modal > .picture {
  position: relative;
  width: calc(60% - 50px);
  height: 100%;
  margin: 70px 20px 70px 50px;
}

.modal > .picture > img {
  border-radius: 15px;
  object-fit: contain;
  margin-bottom: 20px;
}

.modal > .text {
  margin: 70px 50px 70px 20px;
  width: calc(50% - 50px);
}

.modal > .text * {
  font-size: 18px;
}

.modal > .text > .intro {
  padding: 20px 0;
  font-family: 'Pretendard-Regular';
  letter-spacing: -0.5px;
  line-height: 1.5;
}

.modal > .text > ul {
  padding: 20px 0;
}

.modal > .text > ul > li {
  /*height: 40px;*/
  margin-bottom: 10px;
}

.modal > .text > ul > li > .info {
  color: #1a1a1a;
  font-family: 'Pretendard-Regular';
  display: flex;
  justify-content: flex-start;
  /*align-items: center;*/
  flex-direction: row;
  flex-wrap: nowrap;
}

.modal > .text > ul > li > .info > i {
  color: #0e0e0e;
  margin-right: 10px;
}

.modal > .close {
  position: absolute;
  top: 0;
  right: 0;
  margin-right: 20px;
  color: black;
  font-size: 40px;
  cursor: pointer;
}

.modal-overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(0, 0, 0, 0.8);
  z-index: 2;
}

.modal > .fade {
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

.modal > .picture > .image-next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  right: 0;
  width: auto;
  padding: 16px;
  margin-top: -22px;
  color: #6b6b6b;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

.modal > .picture > .image-prev {
  cursor: pointer;
  position: absolute;
  top: 50%;
  left: 0;
  width: auto;
  padding: 16px;
  margin-top: -22px;
  color: #6b6b6b;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

.modal > .picture > .image-next {
  right: 0;
  border-radius: 3px 0 0 3px;
}

.modal > .picture > .image-prev:hover,
.modal > .picture > .image-next:hover {
  background-color: rgba(0, 0, 0, 0.8);
  color: white;
}

.modal > .picture > .dots {
  width: 100%;
  bottom: 10px;
  text-align: center;
}

.modal > .picture > .dots > .dot {
  cursor: pointer;
  height: 4px;
  width: 30px;
  margin: 0 2px;
  background-color: #717171;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.modal > .picture > .dots > .dot.active,
.modal > .picture > .dots > .dot:hover {
  background-color: #ddd;
}

</style>
