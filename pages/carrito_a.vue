<template>
  <v-app>
    <nuxt-link to="/"> Descripción de la prueba</nuxt-link>
      <v-card>
        <h1 style="color: red;">PruebaShop</h1>
      <v-spacer />
      <v-toolbar-title>
          <nuxt-link to="/home_a" class="mx-4">Home</nuxt-link>
          <span class="mr-4">"Hola, {{ $store.state.user.name }}"</span>
          <nuxt-link to="/logout" class="mx-4">Logout</nuxt-link>
          <nuxt-link to="/carrito" class="mx-4">Carrito</nuxt-link>
          <nuxt-link to="/product/create/" class="mr-4">Anadir_Producto</nuxt-link>
          <nuxt-link to="/product/edit/" class="mr-4">Editar_Producto</nuxt-link>
        </v-toolbar-title>
      </v-card>
      <v-main>
        <v-btn color="green" to="/fel_compra">Finalizar compra</v-btn>
      </v-main>
    </v-app>
  </template>

  <script>
   import { mapActions } from "vuex";
   export default {
     middleware: ["auth"],
   };
 </script>