<template>
 <div class="home">
  <Header />
  <HeroCarousel />
  <MainCarousel />
  <InstaPhoto />
  <BrandPartner />
  <Footer />
 </div>
</template>

<script>
import BrandPartner from "../components/home/BrandPartner.vue";
import Footer from "../components/Footer.vue";
import Header from "../components/Header.vue";
import HeroCarousel from "../components/home/HeroCarousel.vue";
import InstaPhoto from "../components/home/InstaPhoto.vue";
import MainCarousel from "../components/home/MainCarousel.vue";

export default {
 name: "Home",
 components: {
  Header,
  HeroCarousel,
  MainCarousel,
  InstaPhoto,
  BrandPartner,
  Footer,
 },
};
</script>
  