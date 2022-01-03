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
      randomCat: null,
    };
  },
  created() {
    // Populate our firebase real time database with data from https://latelier.co/data/cats.json

    /* this.$http
      .get("https://latelier.co/data/cats.json")
      .then((res) => {
        if (res) {
          let data = res.data.images;
          data.forEach((p) => {
            var newValue = { vote: 0 };
            p = { ...p, ...newValue };
            this.$http.post(
              "https://catmash-bbf95-default-rtdb.europe-west1.firebasedatabase.app/cats.json",
              p
            );
          });
        }
      })
      .catch((err) => console.log(err));
 */
    this.$http
      .get(
        "https://catmash-bbf95-default-rtdb.europe-west1.firebasedatabase.app/cats.json"
      )
      .then((res) => {
        if (res) {
          let catArray = [];
          let data = res.data;
          console.log(res.data);
          for (let key in data) {
            data[key].id = key;
            catArray.push(data[key]);
          }
          console.log(catArray);
          let listKeys = Object.keys(catArray);
          let randomIndex = Math.floor(Math.random() * listKeys.length);
          let randomObject = catArray[listKeys[randomIndex]];
          this.randomCat = randomObject;
        }
      })
      .catch((err) => console.log(err));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
