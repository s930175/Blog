<template>
  <i class="fa-solid fa-burger" @click="showMenu"></i>
  <div class="lightBtn" :style="light ? 'display:none' : ''">
    <i class="fa-solid fa-toggle-off" @click="light = true"></i>
  </div>
  <div class="lightBtn" :style="light ? '' : 'display:none'">
    <i class="fa-solid fa-toggle-on" @click="light = false"></i>
  </div>

  <div :class="show == true ? 'container' : 'show'">
    <nav class="menu">
      <div class="manu_container">
        <ul>
          <li><i class="fa-solid fa-angle-right"></i>首頁</li>
          <li><i class="fa-solid fa-angle-right"></i>履歷</li>
          <li><i class="fa-solid fa-angle-right"></i>學習筆記</li>
          <li><i class="fa-solid fa-angle-right"></i>作品集</li>
          <li><i class="fa-solid fa-angle-right"></i>雜談</li>
          <li><i class="fa-solid fa-angle-right"></i>留言給我</li>
        </ul>
      </div>
    </nav>
    <div class="menu-header">123</div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
let show = ref(false);
let light = ref(false);
function showMenu() {
  show.value = !show.value;
}
</script>

<style scoped lang="less">
* {
  margin: 0;
  padding: 0;
  list-style: none;
  box-sizing: border-box;
}
.fa-burger {
  font-size: 2.3rem;
  transform: rotate(-1.5deg);
  z-index: 999;
  padding: 10px;
  position: fixed;
  cursor: grab;
}
.lightBtn{
  text-align: end;
  cursor: pointer;
  font-size: 2.5rem;
}
.show {
  display: none;
}

.container {
  position: relative;
  width: 25vw;
  height: 98vh;
  .menu {
    position: fixed;
    bottom: 60px;
    padding: 6px;
    width: 15%;
    height: 85%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-width: 2px 3px 2px 5px;
    border-radius: 90% 6% 93% 5% / 5% 94% 7% 95%;
    /* 做出傾斜的視覺感 */
    transform: rotate(0.5deg);
    border-style: solid;
    .manu_container {
      width: 96%;
      height: 90%;
      transform: rotate(-0.5deg);
      .fa-angle-right {
        padding-right: 5px;
      }
      li {
        font-family: "Ma Shan Zheng", cursive;
        font-size: 1.4rem;
        font-weight: 500;
        cursor: pointer;
      }
    }
  }
  .menu-header {
    position: fixed;
    width: 80vw;
    height: 85vh;
    background-color: antiquewhite;
    top: 5%;
    left: 16%;
    z-index: -2;
  }
}
</style>