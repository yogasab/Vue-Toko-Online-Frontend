<template>
 <div class="home">
  <Header />
  <Carousel />
 </div>
</template>

<script>
import Header from "../components/Header.vue";
import Carousel from "../components/Carousel.vue";

export default {
 name: "Home",
 components: {
  Header,
  Carousel,
 },
};
</script>
