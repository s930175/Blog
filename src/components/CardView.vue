<template>
  <div class="cards">
    <div class="main-page">
      <h3>
        {{ name }}
      </h3>
      <img :src="src" alt="" />
      <p>屬性:{{ 屬性 }}</p>
    </div>
  </div>
</template>

<script>
import { toRef, ref, reactive } from "vue";

export default {
  props: ["id", "src", "name", "index", "屬性"],

  setup() {},
};
</script>

<style lang="less" scoped>
.cards{
  width: 150px;
}
.main-page {
    text-align: center;
  img {
    max-width: 100%;
  }
}
</style>