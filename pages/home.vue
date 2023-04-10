
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
            <div>
              <v-container>
                <v-simple-table>
                  <template v-slot:default>
                    <thead>
                      <tr>
                        <th class="text-left">Product Id</th>
                        <th class="text-left">Title</th>
                        <th class="text-left">User Id</th>
                        <th class="text-left">Content</th>
                        <th class="text-left">Photo</th>
                        <th class="text-left">Price</th>
                        <th class="text-left">Rate</th>
                        <th class="text-left">Comprar</th>
                      </tr>
                    </thead>
                    <tbody v-if="$store.state.products.length > 0">
                      <tr v-for="product in $store.state.products" :key="product.id">
                        <td>{{ product.id }}</td>
                        <td>{{ product.title }}</td>
                        <td>{{ product.user_id }}</td>
                        <td>{{ product.content }}</td>
                        <td>{{ product.url }}</td>
                        <td>{{ product.price }}</td>
                        <td>{{ product.rate }}</td>
                        <td>
                          <nuxt-link to="/carrito"><v-btn style="background-color:green;" >Anadir al carrito</v-btn></nuxt-link>
                        </td>
                      </tr>
                    </tbody>
                    <tbody v-else>
                      <h3>Record Not Found</h3>
                    </tbody>
                  </template>
                </v-simple-table>
              </v-container>
            </div>
          </v-main>
        </v-app>
  </template>
  
<script>
  
import { mapActions } from "vuex";
export default {
  middleware: ["guest"],
  methods: {
  ...mapActions(["getAllProduct"]),
  },
  mounted() {
    this.getAllProduct();
  },

};
</script>
  
<style>
  a {
    text-decoration: none !important;
  }
</style>