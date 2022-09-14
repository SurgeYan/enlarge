<script setup>
// 使用本组件前 先下载包 npm i @vueuse/core 或 yarn add @vueuse/core 或 pnpm i @vueuse/core
import { ref, computed } from 'vue';
import { useMouseInElement } from '@vueuse/core';

const props = defineProps({
  images: {
    type: Array,
    default: () => [],
  },
});
const target = ref(null);
// isOutside是否进入指定区域 进入为false 否则为true
// elementX 鼠标X位置
// elementY 鼠标Y位置
const { isOutside, elementX, elementY } = useMouseInElement(target); // useMouseInElement(指定的区域)鼠标进入的位置

const position = computed(()=>{
  let x = elementX.value - 100;
  let y = elementY.value - 100;
  x = x < 0 ? 0 : x;
  y = y < 0 ? 0 : y;
  x = x > 200 ? 200 : x;
  y = y > 200 ? 200 : y;
  return {
    x,
    y,
  };
});
  // 给imgSrc默认一个值
const imgSrc = ref('');
function showMainImg(img) {
  imgSrc.value = img;
}
</script>

<template>
  <div class="goods-img">
    <!-- 放大框 -->
    <div
      class="large"
      v-show="!isOutside"
      :style="[{backgroundImage:`url('${ imgSrc ? imgSrc : props.images[0] }')`, backgroundPosition: `-${position.x*2}px -${position.y*2}px`}]"
    />
    <!-- 原始框 -->
    <div class="middle" ref="target">
      <img :src="imgSrc ? imgSrc : props.images[0]" alt="" />
      <!-- 移动遮罩 -->
      <div class="layer" ref="target" v-show="!isOutside " :style="{ left:position.x+'px', top: position.y+'px' }"/>
    </div>
    <!-- 右侧小图 -->
    <div class="sub-img">
      <img
        @mouseenter="showMainImg(img)"
        v-for="img in props.images"
        :key="img"
        :src="img"
        alt="加载失败"
        :class="{ 'sub-img-active': imgSrc === img || (!imgSrc && img === props.images[0]) }"
      >
    </div>
  </div>
</template>
<style scoped lang="scss">
.goods-img {
  width: 100%;
  height: 400px;
  position: relative;
  display: flex;
  z-index: 500;
  .large {
    position: absolute;
    top: 0;
    left: 412px;
    width: 400px;
    height: 400px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    background-repeat: no-repeat;
    // 放大一倍
    background-size: 800px 800px;
    background-color: #f8f8f8;
  }
  .middle {
    width: 400px;
    height: 400px;
    background: #f5f5f5;
    position: relative;
    cursor: move;
    > img{
      width: 400px;
      height: 400px;
    }
    .layer {
      width: 200px;
      height: 200px;
      background: rgba(0,0,0,.2);
      left: 0;
      top: 0;
      // 可以移动
      position: absolute;
    }
  }
  .sub-img {

    > img {
      display: block;
      width: 68px;
      height: 68px;
      margin: 0 0 15px 12px;
      &.sub-img-active {
        cursor: pointer;
        border: 2px solid $cyan;
        box-sizing: border-box;
      }
    }
  }
}
</style>
