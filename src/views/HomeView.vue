<template>
  <NavbarViewVue></NavbarViewVue>
  <PokemonViewVue></PokemonViewVue>
  <CarouselViewVue></CarouselViewVue>
  <!-- <CardViewVue></CardViewVue> -->
  <FooterViewVue></FooterViewVue>
</template>

<script>
// import DontLook from '@/components/DontLook.vue'
import NavbarViewVue from '@/components/NavbarView.vue'
import PokemonViewVue from '@/components/PokemonView.vue'
import CarouselViewVue from '@/components/CarouselView.vue'
import CardViewVue from '@/components/CardView.vue'
import FooterViewVue from '@/components/FooterView.vue'

export default {
  components:{
    NavbarViewVue,
    PokemonViewVue,
    CarouselViewVue,
    CardViewVue,
    FooterViewVue
  }
}
</script>

<style>
  body{
      background:linear-gradient(rgba( 255 , 255 , 255 , 0.3 ), rgba( 255 , 255 , 255 , 0.3 )), url('../img/home.png');
    }


</style>
