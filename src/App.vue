<template>
  <NevHeader></NevHeader>
  <ImageSlider></ImageSlider>
  <div class="section-container">
    <AboutArea></AboutArea>
    <CareerArea></CareerArea>
    <PortfolioArea></PortfolioArea>
    <ServiceArea></ServiceArea>
  </div>
  <FooterArea></FooterArea>
</template>

<script>
import NevHeader from "@/components/NevHeader";
import ImageSlider from "@/components/ImageSlider";
import AboutArea from "@/components/AboutArea";
import PortfolioArea from "@/components/PortfolioArea";
import CareerArea from "@/components/CareerArea";
import ServiceArea from "@/components/ServiceArea";
import FooterArea from "@/components/FooterArea";

export default {
  name: 'App',
  components: {
    FooterArea,
    ServiceArea,
    CareerArea,
    AboutArea,
    ImageSlider,
    NevHeader,
    PortfolioArea
  }
}
</script>

<style>
/* COMMON */
* {
  margin: 0;
  padding: 0;
  font-size: 0;
}

@font-face {
  font-family: 'Pretendard-Regular';
  src: url('https://fastly.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Regular.woff') format('woff');
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: 'Pretendard-bold';
  src: url('https://fastly.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Regular.woff') format('woff');
  font-weight: 400;
  font-style: normal;
}

body {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  word-break: break-all;
  font-family: "Pretendard Variable";

}

img {
  width: 100%;
  height: 100%;
}

a {
  text-decoration: none;
  font-size: 14px;
  text-transform: uppercase;
}

ul {
  list-style-type: none;
}

/* SECTION CONTAINER */
.section-container {
  max-width: 1200px;
  margin: 0 auto;
}

/* SECTION */
section {
  padding: 70px 0;
}

.title {
  font-size: 50px;
  font-weight: bold;
  text-align: center;
  letter-spacing: 3px;
  padding-bottom: 50px;
  font-family: "Montserrat";
}

.title::after {
  content: "";
  display: block;
  width: 100px;
  height: 10px;
  margin: 0 auto;
}

</style>
