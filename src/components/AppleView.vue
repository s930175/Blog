<template>
  <div>
    <!-- 1 -->
    <div class="section text">Lorem ipsum dolor sit amet.</div>
    <!-- 2 -->
    <div id="section2" class="section" :style="{'--scale':progress}" :class="{'sticky':fixClass}">
      <div class="phone">
        <img src="https://picsum.photos/1200/900?random=1" alt="" />
        <div class="rect"></div>
      </div>
    </div>
    <!-- 3 -->
    <div id="section3" class="section" :class="{'static':fixClass}">
      <div class="phone">
        <img src="https://picsum.photos/1200/900?random=1" alt="" />
        <div class="rect"></div>
      </div>
    </div>
    <!-- 4 -->
    <div class="section text">Lorem ipsum dolor sit amet.</div>
  </div>
</template>



<script setup>
import { computed, onMounted, ref } from "vue";
    const progress = ref(0);
    // 取得app的事件及計算座標
    onMounted(() => {
      // 先抓取整個畫面
        const app = document.querySelector('#app')
        // 當滾動時執行
        app.addEventListener('scroll',function(){
          // 臨界點小於h(innerHeight為瀏覽器視窗口的高度)時為最大
          // console.log(app.scrollTop)
            if(app.scrollTop < window.innerHeight){
                //對應到Style 的scale；用JS控制CSS變數
                progress.value = 3
                // 臨界點大於2h(超過第二個vh後縮至最小)
            }else if(app.scrollTop > window.innerHeight*2){
                progress.value = 1
            }else{
                // progress
                // 計算在h~2h之間過渡(progress.value:1~3)，卷軸百分比3-(3-1為中間兩個vh長度)((當前位置長度-整個視窗長度)/整個視窗長度)
                // 3-2(0~1)=(3~1)
                progress.value = 3-2*((app.scrollTop-window.innerHeight)/window.innerHeight)
                console.log(((app.scrollTop-window.innerHeight)/window.innerHeight))
            }
        })
    });

    const fixClass = computed(()=>{
        return progress.value > 1
    })




</script>

<style scoped lang="less">
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
  width: 100vw;
  height: 100vh;
  background-color: white;
  overflow: hidden;
}
.text {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 100px;
}
#section2,
#section3 {
  height: 100vh;
  background-color: black;
}
/* 由大 */
#section2{
  /* position: sticky;
  top: 0;
  left: 0; */
  --scale: 3;
}
/* 到小 */
#section3{
  --scale: 1;
}
.sticky {
  /* sticky把區塊卡在卷軸區域 */
  position: sticky !important;
  top: 0;
  left: 0;
}
.static {
  /* 讓圖片用z-index:-1的方式移動(sticky z-index=-1的意思) */
  position: static !important;
}
.phone {
  position: absolute;
  width: 100%;
  height: 100%;
  transform: scale(var(--scale));
}
.phone > * {
  position: absolute;
  /* 從中心點縮放 */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.phone > img {
  /* 裁切 */
  clip-path: inset(21% 7% round 5%);
  width: 60%;
  height: auto;
}
.phone > .rect {
  width: 50%;
  height: 0;
  padding-top: 25%;
  border: 10px solid #fff;
  border-radius: 10px;
}
</style>