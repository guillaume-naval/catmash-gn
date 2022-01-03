<template>
  <v-app class="main">
    <v-container height="50px" class="wrapper d-flex flex-column align-center">
      <h1 class="text-center">Cat Mash</h1>
      <p class="subtitle-1 font-weight-thin">
        Voter pour le chat le plus mignon <v-icon>mdi-cat</v-icon>
      </p>
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
<style>
.main {
  font-family: "Pacifico", cursive;
}
</style>
