<template>
  <v-app>
    <v-container
      height="50px"
      class="wrapper d-flex flex-column align-center justify-center"
    >
      <h1 class="text-center">CATMASH</h1>
      <p class="subtitle-1">Voter pour le plus mignon !</p>
      <MainMash />
      <Rankings />
    </v-container>
  </v-app>
</template>

<script>
import MainMash from "./components/MainMash";
import Rankings from "./components/Rankings";

export default {
  name: "App",

  components: {
    MainMash,
    Rankings,
  },

  data: () => ({
    //
  }),
};
</script>
<style scoped>
</style>
