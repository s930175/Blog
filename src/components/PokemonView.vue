<template>
  <div class="app">
    <div class="section text start">在故事開始之前......</div>
    <div id="section2" class="section" :class="{ sticky: fixClass }">
      <div class="section bgR" :class="{ static: fixClass }">
        <h2 style="padding: 10px">人物介紹</h2>
        <div class="main-roles">
          <div class="main-role">
            <h3>主角</h3>
            <img class="role" src="../img/主角(仮).png" alt="" />
          </div>
          <div class="Chihuahua">
            <div class="Chihuahua_other">
              <img
                class="Chihuahua_other_role"
                src="../img/臉紅害羞.png"
                alt=""
              />
              159cm 45kg <br />
              性別:玩家選擇
            </div>
            <h3>主角夥伴</h3>
            <div class="Chihuahua_other">
              <img
                class="Chihuahua_other_role_Chihuahua"
                src="../img/吉祥物01.png"
                alt=""
              />
              <div>
                吉祥物 <br>
                HP:50 <br />
                ATK:50<br />
                DEF:20 <br />
                SPD:330
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="section bgG" :class="{ static: fixClass }">
        <h2 style="padding: 10px">故事背景</h2>
        <div>
          <p style="padding: 10px">
            主覺的爺爺糊塗了，聽不懂主角分享的喜怒哀樂；<br />爺爺四肢退化，主角無法牽著他到公園散步；<br />最終，爺爺連吞嚥都沒辦法了，主角甚至沒能為她吃下一口稀飯。<br>
            過去爺爺一手將主角帶大，臨終前主角卻沒能為他做點什麼。主角感嘆自己的無力，同時也迷失了活著的理由。為了給自己的生命找到一點意義，他踏上了目標為尋找目標的旅途。<br>
            性格：文靜、溫柔、願意為他人捨身（不重視自己）、基本上不會生氣（已經沒有更重要的東西可以失去了）
          </p>
        </div>
      </div>
      <div class="section bgB" :class="{ static: fixClass }">
      <h2 style="margin:10px 0 10px 60px">遊戲特色</h2>
      <div style="margin-left:60px">
        <p>劇情:豐富的劇情內容</p>
        <p>蒐集:多種霞精靈可供蒐集</p>
        <p>對戰:PVP策略型對戰</p>
        <p>養成:陪著主角一步步成長</p>
      </div>
      <!-- 這裡也要放圖 -->
      <img class="section-img" src="../img/探索.png" alt="">
      <img class="section-img" src="../img/隊伍.png" alt="">
      <img class="section-img" src="../img/家園.png" alt="">
      <img class="section-img" src="../img/商店.png" alt="">
      </div>
      <div class="section bgB" :class="{ static: fixClass }"></div>
      <div class="section bgB" :class="{ static: fixClass }"></div>
    </div>
    <div class="section bgG" :class="{ static: fixClass }"></div>
    <div class="section bgB" :class="{ static: fixClass }"></div>
    <div class="section text end">
      <br>
      <br>
      有沒有很讚啊? <br>
      接下來看看有那些霞精靈可以蒐集吧!
      <img src="../img/邂逅.png" alt="">
    </div>
    
  </div>
</template>
<!-- 本組件依靠bug運行，此功能從是學(抄)習(襲)來的，bug一堆待解決 -->
<script setup>
import { computed, onMounted, ref } from "vue";
const progress = ref(0);

onMounted(() => {
  const app = document.querySelector("#app");
  const section = document.querySelector("#section2");
  app.addEventListener("scroll", function () {
    if (app.scrollTop < window.innerHeight) {
      //對應到Style 的scale
      progress.value = 0;
    } else if (app.scrollTop > window.innerHeight * 3) {
      progress.value = 1;
    } else {
      // progress
      progress.value =
        (app.scrollTop - window.innerHeight) / (window.innerHeight * 2);
    }
    // 卷軸
    let position = (section.scrollWidth - window.innerWidth) * progress.value;
    section.scrollTo({ left: position });
    // console.log(progress.value)//會輸出運算0~1
  });
});

const fixClass = computed(() => {
  return progress.value < 1;
});
</script>
<!-- 不可下less & scoped，會出現重大bug -->
<style>
* {
  margin: 0;
  padding: 0;
}
body {
  overflow: hidden;
}
#app {
  width: 100vw;
  height: 100vh;
  overflow: auto;
}
.section {
  position: relative;
  width: 100%;
  height: 100%;
  /* background-color: white; */
  font-family: "Ma Shan Zheng", "Caveat", cursive;
  /* overflow: hidden; */
}

.text {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Ma Shan Zheng", "Caveat", cursive;
  font-size: 2.5rem;
}
/* #section2,
#section3 {
   background-color: black; 
} */
/* #section2 {
  --scale: 3;
}
#section3 {
  --scale: 1;
} */
#section2 {
  display: flex;
  flex-wrap: nowrap;
  /* overflow: auto; */
  /* 將卷軸破綻隱藏 */
  overflow: hidden;
}
#section2 > .section {
  width: 100vw;
  min-width: 100vw;
}
.sticky {
  /* sticky把區塊卡在卷軸區域 */
  position: sticky !important;
  top: 0;
  left: 0;
}
.static {
  /* 讓圖片用z-index:-1的方式移動 */
  position: static !important;
  height: 60vh;
}
/* /////////////////////////////// */
.start{
  height: 30vh;
}
.end{
  margin: auto;
  display: flex;
  flex-wrap: wrap;
}
.end img{
  /* width: 80%; */
  height: 50%;
}
.section-img{
  margin: auto;
  max-width: 20%;
}
.main-roles {
  height: inherit;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.main-role {
  width: 40vw;
  height: 100%;
}
.main-role .role {
  max-width: 40vw;
  max-height: 80%;
}
.Chihuahua {
  width: 40vw;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
}
.Chihuahua_other {
  width: 40vw;
  height: 50%;
  display: flex;
  justify-content: space-around;
}
.Chihuahua_other_role,
.Chihuahua_other_role_Chihuahua {
  max-width: 40vw;
  max-height: 75%;
}
.Chihuahua_other_role {
  max-width: 70%;
  height: auto;
  border: 1px solid #000;
  border-radius: 50%;
}

</style>