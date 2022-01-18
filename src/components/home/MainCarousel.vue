<template>
 <!-- Women Banner Section Begin -->
 <section class="women-banner spad">
  <div class="container-fluid">
   <div class="row">
    <div class="col-lg-12 mt-5" v-if="products">
     <carousel
      class="product-slider"
      :items="4"
      :nav="false"
      :autoplay="true"
      :dots="false"
     >
      <div class="product-item" v-for="product in products" :key="product.id">
       <div class="pi-pic">
        <img :src="product.galleries[0].photo" alt="" />
        <ul>
         <li class="w-icon active">
          <a href="#"><i class="icon_bag_alt"></i></a>
         </li>
         <li class="quick-view">
          <!-- <router-link :to="'/product/' + product.id">+ Quick View</router-link> -->
          <router-link :to="{ name: 'Product', params: { id: product.id } }"
           >+ Quick View</router-link
          >
         </li>
        </ul>
       </div>
       <div class="pi-text">
        <div class="catagory-name">{{ product.type }}</div>
        <a href="#">
         <h5>{{ product.name }}</h5>
        </a>
        <div class="product-price">
         Rp{{ product.price }}
         <span>Rp{{ product.price * 0.8 }}</span>
        </div>
       </div>
      </div>
     </carousel>
    </div>

    <div class="col-lg-5" v-else>
     <p>There are no newer products here</p>
    </div>
   </div>
  </div>
 </section>
 <!-- Women Banner Section End -->
</template>


<script>
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
 components: { carousel },
 name: "MainCarousel",
 data() {
  return {
   products: null,
  };
 },
 methods: {
  async getProducts() {
   try {
    const products = await axios.get("http://127.0.0.1:8000/api/v1/products");
    this.products = products.data.data.data;
    console.log(this.products);
   } catch (error) {
    console.log(error);
   }
  },
 },
 mounted() {
  this.getProducts();
 },
};
</script>

<style scoped>
.product-item {
 margin-right: 25px;
}
.pi-pic img {
 height: 450px;
}
</style>