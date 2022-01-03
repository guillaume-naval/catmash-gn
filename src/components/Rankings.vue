<template>
  <v-dialog scrollable transition="dialog-top-transition" width="1000">
    <template
      class="d-flex justify-center align-center"
      v-slot:activator="{ on, attrs }"
    >
      <v-btn color="primary" width="200" v-bind="attrs" v-on="on"
        >Classement</v-btn
      >
    </template>
    <template v-slot:default="dialog">
      <v-card>
        <v-card-text>
          <div class="text-h4 pa-10 text-center">
            Top 5 des chats les plus mignons ! 🐱
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
    return {};
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
