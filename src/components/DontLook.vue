<template>
  <p>{{ a }}</p>
  <p>{{ b }}</p>
  <p>{{ c }}</p>
  <p>{{ arr[0].d }}</p>
  <p>{{ obj.f }}</p>
  <p>----用到ES6----</p>
  <p>{{ h }}</p>
  <p>{{ i }}</p>
  <p>{{ j }}</p>
  <p>{{ k }}</p>
  <p>{{ l }}</p>
  <button @click="handle">click</button>
  <div>firstName: <input type="text" v-model="firstName" /></div>
  <div>lastName: <input type="text" v-model="lastName" /></div>
  <div>{{ fullName }}</div>
  <button @click="update">修改</button>

  <div>str: <input type="text" v-model="str" /></div>
</template>

<script>
import { reactive, ref, toRefs, computed, watch, watchEffect } from "vue";
export default {
  setup() {
    // //////data+methods///////
    let a = ref(1);
    let b = ref(false);
    let c = ref("str");
    let arr = reactive([
      {
        d: 4,
        e: 5,
      },
    ]);
    let obj = reactive({
      f: 7,
      g: 8,
    });
    // 不想.value,也不想在template裡不斷state.···就要用到ES6語法
    let state = reactive({
      h: 10,
      i: 20,
      j: "你看...",
    });
    let state2 = reactive({
      k: 10,
      l: 20,
    });
    // console.log("setup");
    const handle = () => {
      // console.log(handle)
      console.log(obj.f);
      a.value++;
      b.value = !b.value;
      c.value += "--";
      arr[0].d++;
      obj.f++;
      //   下面兩個因為用...state傳出去，所以沒作用
      state.h++;
      state.i++;
      //   下面兩個因為用 ...toRefs(state2)傳出去，所以有作用
      state2.k++;
      state2.l++;
    };
    // //////////computed////////
    let user = reactive({
      firstName: "張",
      lastName: "三",
    });
    // const fullName = computed(() => {
    //   return user.firstName + user.lastName;
    // });
    const fullName = computed({
      get() {
        return user.firstName + user.lastName;
      },
      // 修改執行
      set(value) {
        const names = value.split(" ");
        user.firstName = names[0];
        user.lastName = names[1];
      },
    });
    const update = () => {
      fullName.value = "李 四";
    };
    //////////watch////////////
    const str = ref("abc");
    watch(str, (newValue, oldValue) => {
      console.log(newValue, oldValue);
    });
    // 監聽單個數據
    watch(
      () => user.firstName,
      (newValue, oldValue) => {
        console.log(newValue, oldValue);
      }
    );
    // 監聽多個數據(str及user.firstName)
    // watch(
    //   [str,()=>user.firstName],
    //   (newValue, oldValue) => {
    //     console.log(newValue, oldValue);
    //   }
    // );
    // const fullName = ref("")
    watch(
      [()=>user.firstName,()=>user.lastName],
      (newValue, oldValue) => {
        fullName.value = newValue[0]+""+newValue[1]
      },
    //   立即監聽、深度監聽
    //   {
    //     immediate:true,
    //     deep:true,
    //   }
    );
    watchEffect(()=>{
        fullName.value = user.firstName + " " + user.lastName;
    })
    return {
      a,
      b,
      c,
      arr,
      obj,
      ...state,
      ...toRefs(state2),
      handle,
      ...toRefs(user),
      fullName,
      update,
      str,
    };
  },
};
</script>

<style lang="less" scoped>
</style>
