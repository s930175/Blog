<template>
  <div class="kv" :class="{scroll}">
    <ul class="kvList">
      <li v-for="n in total" :key="n" :style="img(n)" :class="{animate:active===n-1|| preactive===n-1}"></li>
    </ul>
  </div>
</template> 

<script setup>
import { ref } from "vue";

const scroll = ref(false);
const total = ref(5);
const animationDuration = 10;
const active = ref(0);
const preactive = ref(0);


const img = function (n) {
  // console.log(n) 
  // total為5，n in total；n就是1~5
  return {
    backgroundImage: `url(https://picsum.photos/1200/500?random=${n})`,
    animationDuration: `${animationDuration}s`,
    //第二張圖Delay 5s
    // animationDelay: `${((n - 1) * animationDuration) / 2}s`,
    
  };
};

window.addEventListener("scroll", function () {
  //value>0 true ; value=0 false
  scroll.value = (window.scrollY > 0);
});
setInterval(function(){
    preactive.value = active.value
    active.value = (active.value + 1 + total.value) % total.value
},animationDuration/2*1000)
</script>

<style  scoped lang="less">
* {
  margin: 0;
  padding: 0;
}
.kv {
  margin: auto;
  position: relative;
  width: 95vw;
  height: 90vh;
  background-color: transparent;
}
/* 縮小時的畫面 */
.kvList {
  list-style: none;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: transparent;
  /* 中間置中 */
  top: 50%;
  left: 50%;
  /* 記得移回來 */
  transform: translate(-50%, -50%);
  /* 縮小動畫 */
  transition: all 0.5s;
}
.kvList > li {
  /* 圖重疊 */
  position: absolute;
  /* 讓五張圖從一開始就跑 */
  opacity: 0;
  width: 100%;
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: 150% auto;
}
.kvList > li.animate {
  animation-name: kvAnimate;
  animation-timing-function: linear;
  /* animation-iteration-count: infinite; */
}
/* 縮到最小時的範圍 */
.scroll .kvList {
  width: 60vw;
  height: 50vh;
}
@keyframes kvAnimate {
  0% {
    opacity: 0;
    background-size: 150% auto;
  }
  25% {
    opacity: 1;
  }
  50% {
    opacity: 1;
  }
  75% {
    opacity: 0;
  }
  to {
    opacity: 0;
    background-size: 120% auto;
  }
}
</style>


