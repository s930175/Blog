<template>
<NavbarViewVue></NavbarViewVue>
  <div class="LineViewVue">
    <LineViewVue></LineViewVue>
  </div>
  <FooterViewVue></FooterViewVue>

</template>

<script>
// import DontLook from '@/components/DontLook.vue'
import LineViewVue from "@/components/LineView.vue";
import NavbarViewVue from "@/components/NavbarView.vue";
import FooterViewVue from "@/components/FooterView.vue";

export default {
  components: {
    LineViewVue,
    NavbarViewVue,
    FooterViewVue,
  },
};
</script>

<style lang="less" scoped>
*{
  margin: 0;
  padding: 0;
}
.LineViewVue{
  position: absolute;
  top: 2.5%;
  right: 2.5%;
  z-index: -1;
  // opacity: .3;
}
</style>
