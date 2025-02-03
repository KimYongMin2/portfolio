<template>
  <section class="about-area" id="about">
    <div class="title">
      ABOUT
    </div>
    <div class="picture">
      <img src="@/assets/image/about/about-main.jpg">
      <div class="name">김용민</div>
    </div>
    <div class="text">
      <div class="intro">
        안녕하세요! 적응력과 문제해결 능력을 갖춘 개발자 김용민입니다. <br>
        저의 개발은 항상 고객 및 팀원과의 원활한 소통을 중요시하고 <br>
        이를 통하여서 프로젝트의 목표와 요구사항을 명확히 이해하고 반영하려고 노력합니다.<br>
        다양한 환경에서도 유연하게 적응할 수 있는 능력을 가지고 있어 <br>
        새로운 기술이나 도구를 신속하게 학습, 적용하는 데 자신있습니다.
        <br><br>

        Vue.js를 이용한 Front-End 개발에 관해 관심이 많으며 <br>주로 사용하는 언어는 HTML, CSS, JavaScript 입니다.
        <br>
        <br>
      </div>
      <ul>
        <li>
          <div class="info">
            <i class="far fa-calendar-alt"></i> 1996년 3월 4일
          </div>
        </li>
<!--        <li>-->
<!--          <div class="info">-->
<!--            <i class="fas fa-phone"></i> 010 6858 8374-->
<!--          </div>-->
<!--        </li>-->
        <li>
          <div class="info">
            <i class="fas fa-envelope"></i> kym960304@naver.com
          </div>
        </li>
      </ul>
      <!--      <div class="sns">-->
      <!--        <a>-->
      <!--          <i class="fab fa-facebook-f"></i>-->
      <!--        </a>-->
      <!--        <a>-->
      <!--          <i class="fab fa-twitter"></i>-->
      <!--        </a>-->
      <!--        <a>-->
      <!--          <i class="fab fa-linkedin-in"></i>-->
      <!--        </a>-->
      <!--        <a>-->
      <!--          <i class="fab fa-google-plus-g"></i>-->
      <!--        </a>-->
      <!--        <a>-->
      <!--          <i class="fab fa-instagram"></i>-->
      <!--        </a>-->
      <!--      </div>-->
    </div>
  </section>
</template>

<script setup>

</script>

<style scoped>
/* 여기에 필요한 스타일을 추가하세요 */
/* ABOUT AREA */
.about-area {
  height: auto;
  position: relative;
}

.about-area > .picture {
  display: block;
  text-align: center;
  padding: 20px;
}

@media (min-width: 992px) {
  .about-area > .picture {
    width: calc(40% - 40px);
    display: inline-block;
  }
}

.about-area > .picture > img {
  max-width: 400px;
  max-height: 300px;
  border-radius: 15px;
  object-fit: contain;
}

.about-area > .picture > .name {
  font-size: 25px;
  text-align: center;
  padding: 15px 0;
  font-family: 'Pretendard-bold';
}

.about-area > .picture > .description {
  font-size: 14px;
  font-family: 'Pretendard-Regular';
}

.about-area > .text {
  display: block;
  padding: 30px;
}

@media (min-width: 992px) {
  .about-area > .text {
    width: calc(60% - 100px);
    display: inline-block;
    padding: 0 50px;
  }
}

.about-area > .text * {
  font-size: 18px;
}

.about-area > .text > .intro {
  padding: 20px 0;
  font-family: 'Pretendard-Regular';
  letter-spacing: -0.5px;
  line-height: 1.5;
}

.about-area > .text > ul {
  padding: 20px 0;
}

.about-area > .text > ul > li {
  height: 40px;
}

.about-area > .text > ul > li > .info {
  color: #777;
  font-family: 'Pretendard-Regular';
}

.about-area > .text > ul > li > .info > i {
  color: #0e0e0e;
}

.about-area > .text > .sns {
  text-align: right;
}

@media (min-width: 992px) {
  .about-area > .text > .sns {
    text-align: left;
  }
}

.about-area > .text > .sns > a {
  width: 50px;
  line-height: 50px;
  background-color: #eee;
  border-radius: 5px;
  font-size: 16px;
  display: inline-block;
  text-align: center;
  cursor: pointer;
}

.about-area > .text > .sns > a:hover {
  background-image: linear-gradient(to right, royalblue, aquamarine);
}

</style>
