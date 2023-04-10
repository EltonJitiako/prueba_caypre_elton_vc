<template>
    <v-app>
      <div v-if="$store.state.user.name[0]==='('">
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
            <v-row justify="center" align="center">
              <v-col cols="12" sm="8" md="6">
                <v-card>
                  <v-card-title>
                    <h1 class="my-4 text-center">Crear Producto</h1>
                    <form action="" id="w-100" @submit.prevent="create">
                      <v-textField
                        label="Enter the Title"
                        v-model="title"
                        type="text"
                      ></v-textField>
                      <v-textField
                        label="Enter the Content"
                        type="text"
                        v-model="content"
                      ></v-textField>
                      <v-textField
                        label="Enter the Photo(URL)"
                        type="text"
                        v-model="url"
                      ></v-textField>
                      <v-textField
                        label="Enter the Price"
                        type="number"
                        v-model="price"
                      ></v-textField>
                      <v-textField
                        label="Enter the rate"
                        type="number"
                        v-model="rate"
                      ></v-textField>
                      <v-btn color="primary" type="submit">Save</v-btn>
                    </form>
                  </v-card-title>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </div>
      </v-main>
      </div>
      <div v-else>
        <h1>No es admin</h1>
        <nuxt-link to="/home_a" class="mx-4">Home</nuxt-link>
      </div>
    </v-app> 
  </template>

  <script>
  import { mapActions } from "vuex";
  export default {
    middleware: ["auth"],
    data() {
      return {
        title: "",
        content: "",
        url: "",
        price: "",
        rate: "",
      };
    },
    methods: {
      ...mapActions(["createProduct"]),
      create() {
        if (!this.title || !this.content || !this.url || !this.price || !this.rate) {
          alert("Please fill all the field");
        } else {
          const data = {
            title: this.title,
            content: this.content,
            url: this.url,
            price: this.price,
            rate: this.rate,
          };
          this.createProduct(data);
        }
      },
    },
  };
  </script>
  <style>
  #w-100 {
    width: 100%;
  }
  .text-center {
    text-align: center !important;
  }
  </style>