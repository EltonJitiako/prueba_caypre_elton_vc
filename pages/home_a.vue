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
          <nuxt-link to="/carrito_a" class="mx-4">Carrito</nuxt-link>
          <nuxt-link to="/product/create/" class="mr-4">Anadir_Producto</nuxt-link>
          <nuxt-link to="/product/edit/" class="mr-4">Editar_Producto</nuxt-link>
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
                  <nuxt-link to="/carrito_a"><v-btn style="background-color:green;" >Anadir al carrito</v-btn></nuxt-link>
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
    
    middleware: ["auth"],
    methods: {
  ...mapActions(["getAllProduct"]),
  ...mapActions(["deleteProduct"]),
  ...mapActions(["readUser"]),
  deletePro(id) {
    const data = {
      id: id,
    };
    this.deleteProduct(data);
    this.getAllProduct();
  },
},
mounted() {
  this.readUser();
  this.getAllProduct();
},
    

  };
  </script>
  
  <style>
  a {
    text-decoration: none !important;
  }
  </style>