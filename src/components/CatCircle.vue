<template>
  <v-app id="inspire">
    <v-container class="d-flex justify-center">
      <div v-if="randomCat">
        <v-img
          aspect-ratio="1"
          :src="randomCat.url"
          max-height="330"
          width="330"
          alt="image cat"
          class="rounded-circle pa-2"
        >
        </v-img>
      </div>
    </v-container>
  </v-app>
</template>
<script>
export default {
  name: "CatCircle",
  data() {
    return {
      randomCat: {
        url: "http://24.media.tumblr.com/tumblr_m82woaL5AD1rro1o5o1_1280.jpg",
        id: "MTgwODA3MA",
      },
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
