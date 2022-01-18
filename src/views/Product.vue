<template>
 <div class="product">
  <Header />

  <!-- Breadcrumb Section Begin -->
  <div class="breacrumb-section text-left">
   <div class="container">
    <div class="row">
     <div class="col-lg-12">
      <div class="breadcrumb-text product-more">
       <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
       <span>Detail</span>
      </div>
     </div>
    </div>
   </div>
  </div>
  <!-- Breadcrumb Section Begin -->

  <!-- Product Shop Section Begin -->
  <section class="product-shop spad page-details">
   <div class="container">
    <div class="row">
     <div class="col-lg-12">
      <div class="row">
       <div class="col-lg-6">
        <div class="product-pic-zoom">
         <img class="product-big-img" :src="defaultPhoto" alt="" />
        </div>
        <div class="product-thumbs">
         <carousel
          :nav="false"
          :autoplay="false"
          :dots="false"
          class="product-thumbs-track ps-slider"
         >
          <div
           class="pt"
           @click="changeProductPhoto(gallery.photo)"
           :class="gallery.photo === defaultPhoto ? 'active' : ''"
           v-for="gallery in product.galleries"
           :key="gallery.id"
          >
           <img :src="gallery.photo" alt="" />
          </div>
         </carousel>
        </div>
       </div>
       <div class="col-lg-6">
        <div class="product-details text-left">
         <div class="pd-title">
          <span>{{ product.type }}</span>
          <h3>{{ product.name }}</h3>
         </div>
         <div class="pd-desc text-left mt-1" v-html="product.description">
          <h4>Rp{{ product.price }}</h4>
         </div>
         <div class="quantity">
          <router-link to="/cart" class="primary-btn pd-cart"
           >Add To Cart</router-link
          >
         </div>
        </div>
       </div>
      </div>
     </div>
    </div>
   </div>
  </section>
  <!-- Product Shop Section End -->

  <RelatedProduct :product="product"></RelatedProduct>

  <Footer />
 </div>
</template>

<script>
import Footer from "../components/Footer.vue";
import Header from "../components/Header.vue";
import Carousel from "vue-owl-carousel";
import RelatedProduct from "../components/RelatedProduct.vue";
import axios from "axios";
export default {
 name: "Product",
 components: { Header, Footer, Carousel, RelatedProduct },
 data() {
  return {
   defaultPhoto: null,
   product: null,
  };
 },
 methods: {
  changeProductPhoto(photo) {
   this.defaultPhoto = photo;
  },
  async getProduct() {
   const product = await axios.get("http://127.0.0.1:8000/api/v1/products", {
    params: {
     id: this.$route.params.id,
    },
   });
   this.product = product.data.data;
   this.defaultPhoto = product.data.data.galleries[0].photo;
  },
 },
 mounted() {
  this.getProduct();
 },
};
</script>


<style scoped>
.product-thumbs .pt {
 margin-right: 13px;
}
</style>