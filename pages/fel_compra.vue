<template>
    <v-app>
        <v-card>
            <h1>Felicitaciones!</h1>
            <h2>Compra realizada con exito.</h2>
        <nuxt-link to="/home_a">Home</nuxt-link>
      </v-card>
    </v-app>
  </template>

<script>
export default {

  middleware: ["auth"],

};
</script>
    
          
