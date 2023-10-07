<template>
  <div class="wrapper relative-position">
    <p class="absolute-right z-top">ALA bala</p>
  </div>
</template>

<script setup lang="ts">
// import BgImg from 'src/assets/bg.jpg';
</script>

<style scoped lang="scss">
div.wrapper {
  height: 600px;
  width: 100%;
  overflow: hidden;
  color: white;
  background: url('src/assets/bg.jpg');
  background-position: -500px;

  p {
    width: 300px;
  }
}
div.wrapper:after {
  content: '';
  background: blue;
  position: absolute;
  top: 190px;
  left: 0px;
  height: 1000px;
  width: 2000px;
  // -webkit-transform: rotate(-35deg);
  // -moz-transform: rotate(-35deg);
  transform: rotate(65deg);
}
</style>
