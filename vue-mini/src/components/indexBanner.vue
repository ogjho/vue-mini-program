<template>
  <!-- swiper -->
  <swiper :options="swiperOption">
    <swiper-slide v-for="item in bannerData" :key="item.key" >
      <router-link v-if="item.link" :to="item.link">
        <div class="photo">
          <img class="map" :src="item.coverImage"/>
        </div>
      </router-link>
      <div class="photo" v-else>
        <img class="map" :src="item.coverImage"/>
      </div>
    </swiper-slide>
    <div class="swiper-pagination" slot="pagination"></div>
    <div class="swiper-button-prev" slot="button-prev"></div>
    <div class="swiper-button-next" slot="button-next"></div>
  </swiper>
</template>

<script>
import { swiper, swiperSlide } from 'vue-awesome-swiper'
export default {
  name: 'banner',
  components: {
    swiper,
    swiperSlide
  },
  data () {
    return {
      swiperOption: {
        spaceBetween: 30,
        centeredSlides: true,
        autoplay: {
          delay: 2500,
          disableOnInteraction: false
        },
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      }
    }
  },
  props: {
    bannerData: {
      type: Array
    }
  }
}

</script>

<style scoped>
.photo{
  width:100%;
  line-height:0px;
}
.map{
  width:100%;
}
.swiper-button-prev, .swiper-button-next {
  width: 15px;
  height: 25px;
  margin-top: -12px;
  background-size: 15px 25px;
}
</style>

