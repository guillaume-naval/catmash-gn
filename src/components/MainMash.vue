<template>
  <div class="cat_mash">
    <CatCircle />
    <CatCircle />
  </div>
</template>
<script>
import CatCircle from "./CatCircle.vue";
export default {
  components: { CatCircle },
  name: "MainMash",
  data() {
    return {};
  },
  props: {},
};
</script>

<style scoped>
.cat_mash {
  display: flex;
  height: 50%;
}
</style>
