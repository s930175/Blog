<template>
  <i class="fa-solid fa-burger" @click="showMenu"></i>
  <div :class="show == true ? 'container' : 'show'">
    <div class="menu">
      <div class="menu_gameLogo">標題未定
        <img src="" alt="">
      </div>
      <div class="manu_container">
        <ul>
          <li><i class="fa-solid fa-angle-right"></i>故事</li>
          <li><i class="fa-solid fa-angle-right"></i>冒險指南</li>
          <li><i class="fa-solid fa-angle-right"></i>登場人物</li>
          <li><i class="fa-solid fa-angle-right"></i>霞精靈介紹</li>
          <li><i class="fa-solid fa-angle-right"></i>最新資訊</li>
          <li><i class="fa-solid fa-angle-right"></i>商品介紹</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
export default {
  setup() {
    let show = ref(false);

    function showMenu() {
      show.value = !show.value;
    }
    return {
      show,
      showMenu,
    };
  },
};
</script>

<style scoped lang="less">
* {
  margin: 0;
  padding: 0;
  list-style: none;
  box-sizing: border-box;
}
.show {
  display: none;
}
.fa-burger {
  font-size: 2.3rem;
  transform: rotate(-1.5deg);
  z-index: 999;
  padding: 10px;
}
.container {
  position: relative;
  margin: auto;
  width: 98vw;
  height: 35vh;
  .menu {
    position: absolute;
    bottom: 60px;
    padding: 6px;
    width: 97%;
    height: 85%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-width: 2px 3px 2px 5px;
    border-radius: 90% 6% 93% 5% / 5% 94% 7% 95%;
    /* 做出傾斜的視覺感 */
    transform: rotate(1.5deg);
    border-style: solid;

    .menu_gameLogo {
      width: 50%;
      height: 80%;
        // background-color: rgb(84, 152, 212);
      margin-right: 10px;
      transform: rotate(-1.5deg);
      font-family: "Ma Shan Zheng", cursive;
      font-size: 1.5rem;
      font-weight: bold;
      text-align: center;
      img{
        max-width: 100%;
        max-height: 100%;
      }
    }
    .manu_container {
      margin-top: 40px;
      width: 50%;
      height: 90%;
      transform: rotate(-1.5deg);
      .fa-angle-right {
        padding-right: 5px;
      }
      li {
        font-family: "Ma Shan Zheng", cursive;
        font-size: 1.3rem;
        font-weight: 500;
      }
    }
  }
}
</style>