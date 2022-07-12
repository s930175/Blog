<template>
  <div class="card-slider">
    <div class="card-slider-items">
      <transition-group name="flip-list">
        <div
          class="card-slider-item"
          v-for="item in showImages"
          :key="item.id"
          :data-id="item.id"
        >
          <img :src="item.src" />
        </div>
      </transition-group>
    </div>
  </div>
  <div class="btn">
    <button @click="change(now - 1)" class="btnPrev">
      <i class="fa-solid fa-angle-left"></i>
    </button>
    <button @click="change(now + 1)" class="btnNext">
      <i class="fa-solid fa-angle-right"></i>
    </button>
  </div>
  <!-- <div id="main-page">
    <img src="../img/杏鮑菇.png" alt="" />
  </div> -->
  <div class="cards">
    <CardViewVue
      v-for="(item, index) in imgs"
      :key="item.id"
      :="item"
      :index="index"
    ></CardViewVue>
  </div>
</template>

<script>
import CardViewVue from "@/components/CardView.vue";
import { ref, reactive, computed } from "vue";
export default {
  components: {
    CardViewVue,
  },
  setup() {
    /////////////////// data
    let imgs = reactive([
      { id: 1, name: "水母", src: require("../img/水母.png"), 屬性: "水、電" },
      {
        id: 2,
        name: "中部粽",
        src: require("../img/遊戲插畫中部粽.png"),
        屬性: "岩",
      },
      {
        id: 3,
        name: "肥豚",
        src: require("../img/遊戲插畫肥豚.png"),
        屬性: "水、暗",
      },
      {
        id: 4,
        name: "幽靈雞",
        src: require("../img/chickevil.png"),
        屬性: "暗、飛",
      },
      { id: 5, name: "垃圾兔", src: require("../img/garbit.png"), 屬性: "飛" },
      {
        id: 6,
        name: "石礫羊",
        src: require("../img/sheepone.png"),
        屬性: "岩",
      },
      {
        id: 7,
        name: "杏鮑菇",
        src: require("../img/杏鮑菇.png"),
        屬性: "未知",
      },
    ]);
    let now = ref(0);
    let count = ref(0);

    ////////////// computed
    const allImages = computed(() => {
      // 7 + 4(左右各兩張)
      const ary = [];
      const total = imgs.length; //7
      let count;
      // console.log(count)//undefined
      if (total > 0) {
        // while先判斷在執行；ary.length已經是個會自增的變數了，所以while迴圈不用再讓他自增
        while (ary.length < 7 + 4) {
          // 長出很多張圖片;count可以看跑幾輪
          count = Math.floor(ary.length / total);
          // 跑count輪迴圈
          for (let i = 0; i < total; i++) {
            // 幫每張圖片設定新id,避免id重複衝突
            ary.push({
              id: count + "-" + imgs[i].id,
              src: imgs[i].src,
            });
            //  console.log(count);
          }
        }
      }
      return ary;
    });
    // 重新排列剛剛allImages生出來的圖片
    const showImages = computed(() => {
      // 起始值為當前值-4，可以讓起始值的位置固定在最左邊
      const start = now.value - 4;
      // console.log(allImages.value.slice(start).concat(allImages.value.slice(0, start)))
      return (
        allImages.value
          // 切出最後四張
          .slice(start)
          // 再串在最前面，做出頭尾相連的感覺
          .concat(allImages.value.slice(0, start))
      );
    });

    //////////////// methods
    const change = (index) => {
      const limit = allImages.value.length - 1;//抓最後一張
      // console.log(allImages.value[limit])
      // 當前值取代:若傳入-1(第一張的前一張)則回到最後一張；若傳入14則回到第一張
      // console.log(now.value)//0~13
      // console.log(index)//1~14
      now.value = index < 0 ? limit : index > limit ? 0 : index;
    };

    // let main = document.querySelector('#main-page')
    // let pics = document.querySelectorAll(".card-slider-item")
    // for(let i = 0; i<pics.length; i++){
    //   pics[i].addEventListener('click',function lookMonster(){
    //     main.childNodes[0].src = this.childNodes[0].src
    //   })
    // }

    // const lookMonster = () => {
    //   let page = document.querySelector("#main-page");
    //   let pics = document.querySelectorAll(".card-slider-item");
    //   for (let i = 0; i < pics.length; i++) {
    //     console.log(imgs);
    //     // console.log(imgs[i].src);
    //     console.log(pics[i].childNodes[0].src);
    //     page.childNodes[0].src = this.pics[i].childNodes[0].src;
    //   }

    // console.log(page.childNodes[0].src)
    // console.log(pics[0])
    // console.log(pics[0].childNodes[0].src);
    // console.log(page.childNodes[0].src);
    // };
    return {
      imgs,
      now,
      count,
      allImages,
      showImages,
      change,
    };
  },
};
</script>

<style scoped>
button {
  border: none;
  background-color: transparent;
}
.card-slider {
  display: flex;
  width: 100%;
  overflow: hidden;
}
.card-slider-items {
  display: flex;
  width: 100%;
  margin-left: calc(-25% * 2.5);
}
.card-slider-item {
  z-index: 1;
  flex: calc(25% - 20px) 0 0;
  margin: 10px;
  padding: 10px;
}
.card-slider-item:hover {
  width: 800px;
}
.card-slider-item:first-child,
.card-slider-item:last-child {
  z-index: -1;
  visibility: hidden;
  border: transparent;
}

img {
  width: 100%;
  border: transparent;
}

.flip-list-move {
  transition: transform 0.5s;
}
.btn {
  text-align: center;
  margin: 10px;
}
.fa-solid {
  padding: 10px;
  font-size: 1.2rem;
}

.cards {
  float: left;
  margin: 3%;
}
</style>

