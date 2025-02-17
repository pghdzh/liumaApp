<template>
  <v-scale-screen width="1080" height="1920" fullScreen>
    <topNav class="topNav" />
    <RouterView class="routerView" />
    <canvas ref="liveCanvas" class="live2d" />
  </v-scale-screen>
</template>

<script setup>
import VScaleScreen from 'v-scale-screen'
import topNav from "@/components/topNav.vue";
import { RouterView } from "vue-router";
import * as PIXI from "pixi.js";
import { Live2DModel } from "pixi-live2d-display/cubism4";
import { onMounted, onBeforeUnmount, ref } from "vue";

window.PIXI = PIXI; // 为了pixi-live2d-display内部调用

let app; // 存储pixi实例
let model; // 存储live2d实例
const liveCanvas = ref();

const init = async () => {
  app = new PIXI.Application({
    view: liveCanvas.value,
    autoStart: true,
    resizeTo: window,
    backgroundAlpha: 0,
  });
  
  model = await Live2DModel.from("./live2d/nxd1080/Nahida_1080.model3.json");
  model.trackedPointers = [
    { id: 1, type: "pointerdown", flags: true },
    { id: 2, type: "mousemove", flags: true },
  ];
  app.stage.addChild(model);
  model.scale.set(0.14); // 调整缩放比例
};

onMounted(() => {
  init();
});

onBeforeUnmount(() => {
  model?.destroy();
  app?.destroy();
});
</script>

<style scoped lang="scss">
.topNav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  /* 确保导航栏位于最上层 */
}

.routerView {
  width: 100%;
  margin-top: 70px;
  /* 保证导航栏不被遮挡 */
  height: calc(100vh - 70px);
  /* 剩余空间用于 RouterView */
  background-color: white;
}

.live2d {
  position: fixed;
  bottom: -60px;
  right: 10px;
  width: 70vw;
  /* 动态调整宽度 */
  height: 40vh;
  /* 动态调整高度 */
  z-index: 99;
}
</style>
