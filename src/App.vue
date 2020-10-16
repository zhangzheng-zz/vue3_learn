<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div>
    <h2>欢迎XXXX</h2>
    <div>请选择一位XXX</div>
  </div>
  <div>
    <button
      v-for="(item, index) in singer"
      :key="index"
      @click="selectSingerFun(index)"
    >
      {{ index }} : {{ item }}
    </button>
    <div>你选择了【{{ selectSinger }}】</div>
  </div>
</template>

<script lang="ts">
interface SingerData {
  singer: string[];
  selectSinger: string;
  selectSingerFun: (index: number) => void;
}

import {
  defineComponent,
  ref,
  reactive,
  toRefs,
  onRenderTracked,
  onRenderTriggered,
} from "vue";

export default defineComponent({
  name: "App",

  // 使用 ref
  // setup() {
  //   const singer = ref(["邓紫棋", "薛之谦", "李荣浩"]);
  //   const selectSinger = ref("");
  //   const selectSingerFun = (index: number) => {
  //     selectSinger.value = singer.value[index];
  //   };
  //   return {
  //     singer,
  //     selectSinger,
  //     selectSingerFun
  //   };
  // },

  setup() {
    // onRenderTracked((event) => {
    //   console.log("状态跟踪组件----------->");
    //   console.log(event);
    // });

    onRenderTriggered((event) => {
      console.log("状态触发组件--------------->");
      console.log(event);
    });

    const singerData: SingerData = reactive({
      singer: ["邓紫棋", "薛之谦", "李荣浩"],
      selectSinger: "",
      selectSingerFun: (index: number) => {
        singerData.selectSinger = singerData.singer[index];
      },
    });
    const data = toRefs(singerData);
    return {
      ...data,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
