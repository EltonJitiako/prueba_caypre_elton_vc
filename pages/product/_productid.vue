<template>
  <v-app>
    <nuxt-link to="/"> Descripción de la prueba</nuxt-link>
    <v-card>
      <h1 style="color: red;">PruebaShop</h1>  
      <v-spacer />
      <v-toolbar-title>
          <nuxt-link to="/home" class="mx-4">Home</nuxt-link>
          <span class="mr-4">"Hola, {{ $store.state.user.name }}"</span>
          <nuxt-link to="/logout" class="mx-4">Logout</nuxt-link>
          <nuxt-link to="/carrito" class="mx-4">Carrito</nuxt-link>
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
                    <h1 class="my-4 text-center">Editar</h1>
                    <form action="" id="w-100" @submit.prevent="updatePro">
                      <v-textField
                        label="Enter Your id"
                        v-model="id"
                        type="hidden"
                      ></v-textField>
                      <v-textField
                        label="Enter Your Title"
                        v-model="title"
                        type="text"
                      ></v-textField>
                      <v-textField
                        label="Enter Your Content"
                        type="text"
                        v-model="content"
                      ></v-textField>
                      <v-textField
                        label="Enter Your Photo(URL)"
                        type="text"
                        v-model="url"
                      ></v-textField>
                      <v-textField
                        label="Enter Your Price"
                        type="number"
                        v-model="price"
                      ></v-textField>
                      <v-textField
                        label="Enter Your Rate"
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
    </v-app>
</template>

  <script>
  import { mapActions } from "vuex";
  export default {
    middleware: ["auth"],
    data() {
      return {
        id: "",
        title: "",
        content: "",
        url: "",
        price: "",
        rate: "",
      };
    },
  
    methods: {
      async getProductById() {
        const data = {
          id: this.$route.params.productid,
        };
        const res = await this.$axios.post(
          "http://pruebashopelton1.000webhostapp.com/prueba_caypre_elton_back.php/crud-file/get-single-products.php",
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
  
      ...mapActions(["updateProduct"]),
      updatePro() {
        if (!this.title || !this.price || !this.content || !this.url || !this.rate) {
          alert("Please Fill the Field");
        } else {
          const data = {
            id: this.id,
            title: this.title,
            content: this.content,
            url: this.url,
            price: this.price,
            rate: this.rate,
          };
          this.updateProduct(data);
        }
      },
    },
    mounted() {
      this.getProductById();
    },
  };
  </script>