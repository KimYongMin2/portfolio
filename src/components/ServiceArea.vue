<template>
  <section class="service-area" id="service">
    <div class="title">SERVICE</div>
    <div class="filter">
      <ul class="filerList list">
        <li class="listItem" :class="{'active': currentListFilter === 'all'}" @click="listFilterSelection('all')">ALL
        </li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentListFilter === 'front'}" @click="listFilterSelection('front')">
          FRONT
        </li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentListFilter === 'back'}" @click="listFilterSelection('back')">
          BACK
        </li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentListFilter === 'git'}" @click="listFilterSelection('git')">GIT
        </li>
        <li class="listItemSlash">|</li>
        <li class="listItem" :class="{'active': currentListFilter === 'communication'}"
            @click="listFilterSelection('communication')">COMMUNICATION
        </li>
      </ul>

      <!--      <ul class="list">-->
      <!--        <li class="listItem" :class="{'active': currentFilter === 'icon'}" @click="filterSelection('icon')">ICON</li>-->
      <!--        <li class="listItem" :class="{'active': currentFilter === 'list'}" @click="filterSelection('list')">LIST</li>-->
      <!--      </ul>-->
    </div>
    <div class="container">
      <a class="review-prev" @click="plusReviewSlides()">&#10094;</a>
      <a class="review-next" @click="plusReviewSlides()">&#10095;</a>
      <div v-for="(slide, index) in filteredReviewItems" :key="index" class="review-slide"
           :class="getSlideClass(index)">
        <div>
          <div class="image">
            <i :class="slide.class"></i>
          </div>
          <div class="name">{{ slide.name }}</div>
        </div>
        <!--        <div class="job">{{ slide.job }}</div>-->
        <div class="text">
          <div class="content">{{ slide.text }}</div>
        </div>
        <!--        <div class="rating">-->
        <!--          <span v-for="star in slide.rating" :key="star" :class="star"></span>-->
        <!--        </div>-->
      </div>
    </div>
    <!--    <div class="container">-->
    <!--      <div class="item" v-for="(slide, index) in filteredReviewItems" :key="index">-->
    <!--        <div class="icon"><span><i :class="slide.class"></i></span></div>-->
    <!--        <div class="service">{{ slide.name }}</div>-->
    <!--        <div class="content">{{ slide.text }}</div>-->
    <!--      </div>-->
    <!--    </div>-->
  </section>
</template>

<script setup>
import {ref, onMounted, computed} from 'vue';

const reviewSlides = ref([
  {
    class: 'fab fa-js-square',
    name: 'Javascript',
    text: 'Javascript를 이용하여 코드를 작성 및 화면을 구성할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star-half-alt'],
    filters: 'front'
  },
  {
    class: 'fa-brands fa-html5',
    name: 'Html',
    text: '기본 HTML 태그 또는 기존 코드를 활용하여 화면을 구성 할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fa-brands fa-css3-alt',
    name: 'Css',
    text: '기본 CSS 사용 및 기존 CSS를 활용하여 레이아웃을 만들 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fa-brands fa-java',
    name: 'Java',
    text: '학생시절 배웠던 언어로 기본적인 CRUD 프로그램을 구성할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'back'
  },
  {
    class: 'fa-brands fa-vuejs',
    name: 'Vue',
    text: 'Vue를 활용한 화면구성 및 웹 개발을 할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fab fa-js',
    name: 'Axios Ajax',
    text: 'Axios, Ajax를 사용하여 서버와 데이터를 주고받을 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fab fa-js',
    name: 'JQuery',
    text: 'JQuery를 사용하여 동적인 페이지를 만들 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fa-solid fa-leaf',
    name: 'Spring-boot',
    text: '기본적인 환경에서 개발 및 프로젝트를 진행할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'back'
  },
  {
    class: 'fa-brands fa-envira',
    name: 'Thymeleaf',
    text: 'Thymeleaf를 통해 화면에 내용을 동적으로 표시할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'front'
  },
  {
    class: 'fa-solid fa-database',
    name: 'Mysql',
    text: 'Mysql를 통해 기본적인 CRUD를 작업할 수 있습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'back'
  },
  {
    class: 'fa-brands fa-github',
    name: 'Github',
    text: '개인적인 용도의 코드의 저장을 위해 사용하였습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'git'
  },
  {
    class: 'fa-brands fa-gitlab',
    name: 'Gitlab',
    text: '외부 저장 및 협업을 위해 git과 동일하게 사용하였습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'git'
  },
  {
    class: 'fa-brands fa-jira',
    name: 'Jira',
    text: '외부 및 회사 프로젝트 관리를 위해 사용하였습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'communication'
  },
  {
    class: 'fa-brands fa-slack',
    name: 'Slack',
    text: '외부 및 회사 커뮤니케이션을 위해 사용하였습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'communication'
  },
  {
    class: 'fa-solid fa-bolt',
    name: 'Flow',
    text: '외부 및 회사 커뮤니케이션을 위해 사용하였습니다.',
    rating: ['fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star', 'fas fa-star'],
    filters: 'communication'
  }
]);

const reviewSlideIndex = ref(0);
// let reviewTimer;

const plusReviewSlides = () => {
  // clearInterval(reviewTimer);
  reviewSlideIndex.value += 1;
  if (reviewSlideIndex.value * 6 > filteredReviewItems.value.length - 1) {
    reviewSlideIndex.value = 0
  }
  showReviewSlides();
  // reviewTimer = setInterval(() => plusReviewSlides(), 3000);
};

const showReviewSlides = () => {
  if (reviewSlideIndex.value > filteredReviewItems.value.length - 1) {
    reviewSlideIndex.value = 0;
  }
  if (reviewSlideIndex.value < 0) {
    reviewSlideIndex.value = filteredReviewItems.value.length - 1;
  }
};

const getSlideClass = (index) => {
  if (((reviewSlideIndex.value * 6) - 1 < index) && (index < (reviewSlideIndex.value + 1) * 6)) {
    return 'show'
  } else {
    return 'hide'
  }
};

const currentListFilter = ref('all');
// const currentFilter = ref('icon');


// function filterSelection(filter) {
//   currentFilter.value = filter;
// }

function listFilterSelection(filter) {
  reviewSlideIndex.value = 0;
  currentListFilter.value = filter;
}

const filteredReviewItems = computed(() => {
  if (currentListFilter.value === 'all') return reviewSlides.value;
  return reviewSlides.value.filter(item => item.filters.includes(currentListFilter.value));
});


onMounted(() => {
  // reviewTimer = setInterval(() => plusReviewSlides(), 3000);
});
</script>

<style scoped>
/* 스타일 추가 */
</style>
