<template>
  <v-app>
    <nuxt-link to="/"> Descripción de la prueba</nuxt-link>
      <v-card>
        <h1 style="color: red;">PruebaShop</h1>
      <v-spacer />
        <v-toolbar-title>
          <nuxt-link to="/home" class="mx-4">Home</nuxt-link>
          <nuxt-link to="/login" class="mx-4">Login</nuxt-link>
          <nuxt-link to="/signup" class="mx-4">Signup</nuxt-link>
          <nuxt-link to="/carrito" class="mx-4">Carrito</nuxt-link>
        </v-toolbar-title>
      </v-card>
      <v-main>
        <span>{{ this.$shop }}</span>
        <v-btn color="green" to="/fel_compra">Finalizar compra</v-btn>
        </v-main>
    </v-app>
  </template>
   <script>

     import { mapActions } from "vuex";
     export default {
    middleware: ["guest"],


      methods: {
      async getProductById() {
        const data = {
          id: this.$route.params.productid,
        };
        const res = await this.$axios.post(
          "http://localhost/prueba_caypre_elton_back.php/crud-file/get-single-products.php",
          data
        );
        if (res.data.status == 1) {
          this.id = res.data.message[0].id;
          this.title = res.data.message[0].title;
          this.content = res.data.message[0].content;
          this.url = res.data.message[0].url;
          this.price = res.data.message[0].price;
          this.rate = res.data.message[0].rate;
        }
      },
    },
mounted() {
  this.getProductById();
},
methods: {
  copy (id) {
      state.shop=id;
      alert(state.shop);
      
  },
  ...mapActions(["getAllProduct"]),
  
  
},
mounted() {
  this.getAllProduct();
},

};
 </script>