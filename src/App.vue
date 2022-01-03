<template>
  <v-app>
    <v-container height="50px" class="wrapper d-flex flex-column align-center">
      <h1 class="text-center">CATMASH</h1>
      <p class="subtitle-1">Voter pour le plus mignon !</p>
      <Cat-circle />
      <Rankings />
    </v-container>
  </v-app>
</template>

<script>
import Rankings from "./components/Rankings";
import CatCircle from "./components/Cat-circle.vue";

export default {
  name: "App",

  components: {
    CatCircle,
    Rankings,
  },

  data: () => ({
    //
  }),
};
</script>
<style scoped>
</style>
