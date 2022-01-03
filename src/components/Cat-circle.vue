<template>
  <v-container class="d-flex justify-center">
    <v-alert class="alert" v-if="isHidden">Merci pour le vote! 😋</v-alert>
    <div v-if="randomCat1" class="randcat1">
      <v-img
        aspect-ratio="1"
        :src="randomCat1.url"
        alt="image cat"
        class="cat-avatar rounded-circle pa-2"
        @click="
          addVote(randomCat1.id);
          isHidden = !isHidden;
        "
      >
      </v-img>
    </div>
    <p class="vs">vs</p>
    <div v-if="randomCat2" class="randcat2">
      <v-img
        aspect-ratio="1"
        :src="randomCat2.url"
        alt="image cat"
        class="cat-avatar rounded-circle pa-2"
        @click="
          addVote(randomCat2.id);
          isHidden = !isHidden;
        "
      >
      </v-img>
    </div>
  </v-container>
</template>
<script>
export default {
  name: "Cat-circle",
  data() {
    return {
      isHidden: false,
      randomCat1: null,
      randomCat2: null,
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
          this.randomCat1 = catArray[listKeys[randomIndex]];
          this.randomCat2 = catArray[listKeys[randomIndex + 1]];
        }
      })
      .catch((err) => console.log(err));
  },
  methods: {
    addVote(id) {
      console.log(id);
      this.$http
        .get(
          "https://catmash-bbf95-default-rtdb.europe-west1.firebasedatabase.app/cats/" +
            id +
            ".json"
        )
        .then((res) => {
          console.log(res);
          let newVote = res.data.vote + 1;
          console.log(res.data.id);
          console.log(res.data.url);
          this.$http
            .put(
              "https://catmash-bbf95-default-rtdb.europe-west1.firebasedatabase.app/cats/" +
                id +
                ".json",
              { id: res.data.id, url: res.data.url, vote: newVote }
            )
            .then((res) => {
              console.log(res);
            });
        })
        .catch((err) => console.log(err));
      window.setTimeout(function () {
        location.reload();
      }, 500);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alert {
  display: flex;
  position: absolute;
  width: 200px;
  justify-content: center;
  background-color: white;
  box-shadow: 10px 5px 5px rgba(0, 0, 0, 0.548);
  z-index: 4;
}
.cat-avatar {
  width: 300px;
}
.cat-avatar:hover + .hide {
  color: rgb(59, 59, 59) (128, 128, 128, 0.479);
}
.randcat1,
.randcat2 {
  padding: 3em;
}
.vs {
  font-size: 4em;
  padding: 0;
  z-index: 4;
  position: relative;
  top: 140px;
}
@media screen and (max-width: 770px) {
  .cat-avatar {
    width: 200px;
  }
  .randcat1,
  .randcat2 {
    padding: 1.5em;
  }
  .vs {
    font-size: 2.5em;
    top: 90px;
  }
}
@media screen and (max-width: 480px) {
  .cat-avatar {
    width: 150px;
  }
  .randcat1,
  .randcat2 {
    padding: 0.5em;
  }
  .vs {
    font-size: 1.5em;
    top: 60px;
  }
}
</style>
