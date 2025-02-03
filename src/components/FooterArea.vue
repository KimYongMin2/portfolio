<template>
  <footer class="footer-area">
    <div class="info">
      <p>© 2025 Kimyongmin. All rights reserved.</p>
    </div>
  </footer>
</template>

<script setup>

</script>

<style scoped>
/* 여기에 필요한 스타일을 추가하세요 */
/* FOOTER AREA */
.footer-area {
  height: auto;
  text-align: center;
  background-color: black;
}

.footer-area * {
  color: white;
}

.footer-area > .sns > .item {
  display: inline-block;
  padding: 10px;
  cursor: pointer;
}

.footer-area > .sns > .item > i {
  font-size: 24px;
}

.footer-area > .info > p {
  font-size: 16px;
  padding: 40px 0;
  font-family: "Montserrat";
}

</style>
