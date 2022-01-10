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
import BrandPartner from "../components/BrandPartner.vue";
import Footer from "../components/Footer.vue";
import Header from "../components/Header.vue";
import HeroCarousel from "../components/HeroCarousel.vue";
import InstaPhoto from "../components/InstaPhoto.vue";
import MainCarousel from "../components/MainCarousel.vue";

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
  