<template>
  <v-dialog scrollable transition="dialog-top-transition" width="1000">
    <template
      class="d-flex justify-center align-center"
      v-slot:activator="{ on, attrs }"
    >
      <v-btn
        class="text-capitalize"
        elevation="2"
        outlined
        rounded
        color="secondary"
        @click="refreshRanks()"
        width="150"
        v-bind="attrs"
        v-on="on"
        >Classement<v-icon right> mdi-chart-bar </v-icon></v-btn
      >
    </template>
    <template v-slot:default="dialog">
      <v-card>
        <v-card-text>
          <div class="top mt-10 text-center">
            Top 5 des chats les plus mignons
          </div>
          <div v-if="cats" class="d-flex justify-center">
            <div
              class="d-flex flex-column justify-center align-center pa-2"
              v-for="(cat, index) in cats.slice(0, 5)"
              :key="cat.id"
            >
              <p class="rank">{{ index + 1 }}</p>
              <v-img
                :src="cat.url"
                height="150"
                max-width="150"
                alt="image cat"
                class="rounded-circle"
              >
              </v-img>
              <p class="vote font-weight-bold" v-if="cat.vote > 1">
                {{ cat.vote }} votes
              </p>
              <p class="font-weight-bold" v-else>{{ cat.vote }} vote</p>
            </div>
          </div>
        </v-card-text>
        <v-card-actions class="justify-end">
          <v-btn text @click="dialog.value = false">Fermer</v-btn>
        </v-card-actions>
      </v-card>
    </template>
  </v-dialog>
</template>
<script>
export default {
  name: "Rankings",
  data() {
    return {
      ranks: 0,
      cats: null,
    };
  },
  methods: {
    refreshRanks() {
      this.$http
        .get(
          "https://catmash-bbf95-default-rtdb.europe-west1.firebasedatabase.app/cats.json"
        )
        .then((res) => {
          if (res) {
            let catArray = [];
            let data = res.data;
            for (let key in data) {
              data[key].id = key;
              catArray.push(data[key]);
            }
            this.cats = catArray;
            catArray.sort((a, b) => (a.vote > b.vote ? -1 : 1));
            console.log(catArray);
          }
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.rank {
  position: relative;
  top: 50px;
  right: 50px;
  z-index: 4;
  padding: 0em 0.4em 0.2em 0.4em;
  font-size: 1.5em;
  border: 2px solid #666;
  color: #666;
  font-weight: bold;
  text-align: center;
  background-color: white;
  border-radius: 50%;
}
.top {
  font-size: 2em;
}
.vote {
  font-size: 1.4em;
}
</style>
