<template>
 <div class="home">
  <Header />
  <HeroCarousel />
  <MainCarousel></MainCarousel>
 </div>
</template>

<script>
import Header from "../components/Header.vue";
import HeroCarousel from "../components/HeroCarousel.vue";
import MainCarousel from "../components/MainCarousel.vue";

export default {
 name: "Home",
 components: {
  Header,
  HeroCarousel,
  MainCarousel,
 },
};
</script>
