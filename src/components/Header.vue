<template>
 <div class="home">
  <!-- Header Section Begin -->
  <header class="header-section">
   <div class="header-top">
    <div class="container">
     <div class="ht-left">
      <div class="mail-service">
       <i class="fa fa-envelope"></i> hello.shayna@gmail.com
      </div>
      <div class="phone-service"><i class="fa fa-phone"></i> +628 22081996</div>
     </div>
    </div>
   </div>
   <div class="container">
    <div class="inner-header">
     <div class="row">
      <div class="col-lg-2 col-md-2">
       <div class="logo">
        <router-link to="/">
         <img src="img/logo_website_shayna.png" alt="" />
        </router-link>
       </div>
      </div>
      <div class="col-lg-7 col-md-7"></div>
      <div class="col-lg-3 text-right col-md-3">
       <ul class="nav-right">
        <li class="cart-icon">
         Keranjang Belanja &nbsp;
         <a href="#">
          <i class="icon_bag_alt"></i>
          <span>{{ carts.length }}</span>
         </a>
         <div class="cart-hover">
          <div class="select-items">
           <table>
            <tbody v-if="carts">
             <tr v-for="cart in carts" :key="cart.id">
              <td class="si-pic">
               <img :src="cart.photo" alt="" class="cart-gallery" />
              </td>
              <td class="si-text">
               <div class="product-selected">
                <p>Rp{{ cart.price }}</p>
                <h6>{{ cart.name }}</h6>
               </div>
              </td>
              <td class="si-close">
               <i class="ti-close" @click="removeCart(cart.id)"></i>
              </td>
             </tr>
            </tbody>

            <tbody v-else>
             <tr>
              <td class="">
               <p>No products yet</p>
              </td>
             </tr>
            </tbody>
           </table>
          </div>
          <div class="select-total">
           <span>total:</span>
           <h5>Rp{{ prices }}</h5>
          </div>
          <div class="select-button">
           <a href="#" class="primary-btn view-card">
            <router-link to="/cart" style="color: #fff">
             VIEW CARD
            </router-link>
           </a>
           <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
          </div>
         </div>
        </li>
       </ul>
      </div>
     </div>
    </div>
   </div>
  </header>
  <!-- Header End -->
 </div>
</template>

<script>
export default {
 name: "Header",
 data() {
  return {
   carts: [],
   prices: null,
  };
 },
 methods: {
  getCart() {
   if (localStorage.getItem("carts")) {
    try {
     this.carts = JSON.parse(localStorage.getItem("carts"));
    } catch (error) {
     console.log(error);
    }
   }
  },
  removeCart(idx) {
   let userCarts = JSON.parse(localStorage.getItem("carts"));
   let a = userCarts.map((cart) => cart.id);

   let index = a.findIndex((id) => id === idx);
   this.carts.splice(index, 1);
   this.addToCart();
  },
  addToCart() {
   const parsedCart = JSON.stringify(this.carts);
   localStorage.setItem("carts", parsedCart);
  },
  totalPrice() {
   this.prices = this.carts.reduce(function (items, data) {
    return items + data.price;
   }, 0);
  },
 },
 mounted() {
  this.getCart();
  this.totalPrice();
 },
};
</script>

<style scoped>
.cart-gallery {
 width: 80px;
 height: 80px;
}
</style>