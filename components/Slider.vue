<template>
  <div :class="`${background} swiper`">
    <div v-swiper:mySwiper="options">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="banner in banners" :key="banner">
          <img :src="banner" class="swiper-image">
        </div>
      </div>
    </div>
    <div class="swiper-pagination" slot="pagination"></div>
    <div class="swiper-button-prev" slot="button-prev"></div>
    <div class="swiper-button-next" slot="button-next"></div>
  </div>
</template>
<script>
import { directive } from "vue-awesome-swiper";
import "swiper/css/swiper.css";

export default {
  directives: {
    swiper: directive
  },
  props: {
    imgs: Array,
    background: String
  },
  data: function() {
    return {
      banners: this.imgs,
      options: {
        slidesPerView: 1,
        loop: true,
        speed: 500,
        autoplay: {
          delay: 5000,
        },
        pagination: {
          el: ".swiper-pagination"
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev"
        }
      }
    };
  }
};
</script>
<style lang="scss" scoped>
@import "./assets/_mixins.scss";
.swiper {
  position: relative;
  width: 100%;
  &:hover{
    cursor: grab;
  }
  &:active{
    cursor: grabbing;
  }
  .swiper-image {
    width: 100%;
  }
  .swiper-pagination {
    bottom: -18px;
    left: 0;
  }
  .swiper-button-prev,
  .swiper-button-next {
    top: auto;
    width: 30px;
    height: 30px;
    bottom: -30px;
    color: $black;
    left: auto;
    &:after {
      font-size: 12px;
    }
  }
  .swiper-button-prev {
    right: 40px;
  }
  .swiper-button-next {
    right: -10px;
  }
  &.dark {
    .swiper-button-prev,
    .swiper-button-next {
      color: white;
    }
  }
  &.about-slider{
    .swiper-pagination, .swiper-button-prev, .swiper-button-next{
      display: none;
      @include bp(s720){
        display: flex;
      }
    }
    .swiper-image{
      filter: grayscale(1);
      opacity: 0.6;
      transition: all 0.3s;
      &:hover {
        filter: grayscale(0);
        opacity: 1;
      }
    }
  }
}
</style>