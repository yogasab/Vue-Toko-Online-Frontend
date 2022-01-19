<template>
 <div class="shopping">
  <Header />
  <!-- Breadcrumb Section Begin -->
  <div class="breacrumb-section">
   <div class="container">
    <div class="row">
     <div class="col-lg-12">
      <div class="breadcrumb-text product-more text-left">
       <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
       <span>Shopping Cart</span>
      </div>
     </div>
    </div>
   </div>
  </div>
  <!-- Breadcrumb Section Begin -->

  <!-- Shopping Cart Section Begin -->
  <section class="shopping-cart spad">
   <div class="container">
    <div class="row">
     <div class="col-lg-8">
      <div class="row">
       <div class="col-lg-12">
        <div class="cart-table">
         <table>
          <thead>
           <tr>
            <th>Image</th>
            <th class="p-name text-center">Product Name</th>
            <th>Price</th>
            <th>Action</th>
           </tr>
          </thead>
          <tbody v-for="product in carts" :key="product.id">
           <tr>
            <td class="cart-pic first-row">
             <img :src="product.photo" />
            </td>
            <td class="cart-title first-row text-center">
             <h5>{{ product.name }}</h5>
            </td>
            <td class="p-price first-row">Rp{{ product.price }}</td>
            <td class="delete-item">
             <a href="#"><i class="material-icons"> close </i></a>
            </td>
           </tr>
          </tbody>
         </table>
        </div>
       </div>
       <div class="col-lg-12 text-left">
        <h4 class="mb-4">Informasi Pembeli:</h4>
        <div class="user-checkout">
         <form>
          <div class="form-group">
           <label for="namaLengkap">Nama lengkap</label>
           <input
            type="text"
            class="form-control"
            id="namaLengkap"
            aria-describedby="namaHelp"
            placeholder="Masukan Nama"
            v-model="form.name"
           />
          </div>
          <div class="form-group">
           <label for="namaLengkap">Email Address</label>
           <input
            type="email"
            class="form-control"
            id="emailAddress"
            aria-describedby="emailHelp"
            placeholder="Masukan Email"
            v-model="form.email"
           />
          </div>
          <div class="form-group">
           <label for="namaLengkap">No. HP</label>
           <input
            type="text"
            class="form-control"
            id="noHP"
            aria-describedby="noHPHelp"
            placeholder="Masukan No. HP"
            v-model="form.phone_number"
           />
          </div>
          <div class="form-group">
           <label for="alamatLengkap">Alamat Lengkap</label>
           <textarea
            class="form-control"
            id="alamatLengkap"
            rows="3"
            v-model="form.address"
           ></textarea>
          </div>
         </form>
        </div>
       </div>
      </div>
     </div>
     <div class="col-lg-4">
      <div class="row">
       <div class="col-lg-12">
        <div class="proceed-checkout text-left">
         <ul>
          <li class="subtotal">ID Transaction <span>#SH12000</span></li>
          <li class="subtotal mt-3">
           Subtotal <span>Rp{{ price }}</span>
          </li>
          <li class="subtotal mt-3">
           Pajak <span>10% of Rp{{ price }}</span>
          </li>
          <li class="subtotal mt-3">
           Total Biaya <span>Rp{{ totalPrice }}</span>
          </li>
          <li class="subtotal mt-3">Bank Transfer <span>Mandiri</span></li>
          <li class="subtotal mt-3">
           No. Rekening <span>2208 1996 1403</span>
          </li>
          <li class="subtotal mt-3">Nama Penerima <span>Shayna</span></li>
         </ul>
         <a href="#" @click="submitTransactionForm(form)" class="proceed-btn"
          >I ALREADY PAID</a
         >
        </div>
       </div>
      </div>
     </div>
    </div>
   </div>
  </section>
  <!-- Shopping Cart Section End -->
 </div>
</template>

<script>
import Header from "../components/Header.vue";
import axios from "axios";
export default {
 name: "ShoppingCart",
 components: { Header },
 data() {
  return {
   carts: [],
   form: {
    name: "",
    email: "",
    address: "",
    phone_number: "",
    transaction_status: "PENDING",
   },
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
  submitTransactionForm(form) {
   const transaction_details = this.carts.map((cart) => {
    return cart.id;
   });
   const transaction_total = this.totalPrice;
   const transaction = { ...form, transaction_details, transaction_total };

   axios
    .post("http://127.0.0.1:8000/api/v1/checkouts", transaction)
    .then(() => {
     localStorage.removeItem("carts");
     this.$router.push("success");
    })
    .catch((error) => console.log(error));
  },
 },
 mounted() {
  this.getCart();
 },
 computed: {
  price() {
   return this.carts.reduce(function (items, data) {
    return items + data.price;
   }, 0);
  },
  discountPrice() {
   return (this.price * 10) / 100;
  },
  totalPrice() {
   return this.price + this.discountPrice;
  },
 },
};
</script>