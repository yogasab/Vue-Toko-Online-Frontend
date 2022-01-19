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
          <a href="#">
           <i
            class="icon_bag_alt"
            @click="
             addToCart(
              product.id,
              product.name,
              product.price,
              product.galleries[0].photo
             )
            "
           >
           </i
          ></a>
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
   carts: [],
  };
 },
 methods: {
  async getProducts() {
   try {
    const products = await axios.get("http://127.0.0.1:8000/api/v1/products");
    this.products = products.data.data.data;
   } catch (error) {
    console.log(error);
   }
  },
  getCart() {
   if (localStorage.getItem("carts")) {
    try {
     this.carts = JSON.parse(localStorage.getItem("carts"));
    } catch (error) {
     localStorage.removeItem("carts");
    }
   }
  },
  addToCart(id, name, price, photo) {
   let storedProduct = {
    id,
    name,
    price,
    photo,
   };
   // Add new stored product object to carts array
   this.carts.push(storedProduct);
   // Parse to string before set to Local Storage
   const parsedCarts = JSON.stringify(this.carts);
   // Set to Local Storage
   localStorage.setItem("carts", parsedCarts);
   window.location.reload();
  },
 },
 mounted() {
  this.getProducts();
  this.getCart();
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