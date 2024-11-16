<script setup lang="ts">
import { ref } from 'vue'
import type { BannerItem } from '@/types/home'

const activeIndex = ref(0)
const onChange: UniHelper.SwiperOnChange = (ev) => {
  // ! 非空断言，主观上排除掉空值情况
  activeIndex.value = ev.detail!.current
}
// 定义 props 接收
defineProps<{
  list: BannerItem[]
}>()
</script>

<template>
  <view class="carousel">
    <swiper :circular="true" :autoplay="true" :interval="3000" @change="onChange">
      <swiper-item v-for="item in list" :key="item.id">
        <navigator :url="item.hrefUrl" hover-class="none" class="navigator">
          <image mode="aspectFill" class="image" :src="item.imgUrl"></image>
        </navigator>
      </swiper-item>
    </swiper>
    <view class="indicator">
      <text
        v-for="(item, index) in list"
        :key="item.id"
        class="dot"
        :class="{ active: index === activeIndex }"
      ></text>
    </view>
  </view>
</template>

<style scoped lang="scss">
.carousel {
  position: relative;
  height: 200rpx;

  .navigator {
    height: 100%;
  }

  .indicator {
    position: absolute;
    bottom: 10rpx;
    display: flex;
    width: 100%;
    justify-content: center;

    .dot {
      width: 20rpx;
      height: 3rpx;
      margin: 0 5rpx;
      border-radius: 3rpx;
      background-color: rgba(200, 200, 200, 0.3);

      &.active {
        background-color: #fff;
      }
    }
  }
}
</style>
