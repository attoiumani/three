<template>

          <swiper ref="mySwiper" :options="swiperOptions">
            <swiper-slide>
              <div class="my-project">
                <img class="img-fluid" src="https://fakeimg.pl/250x250" alt>
              </div>
            </swiper-slide>
            <swiper-slide>
              <div class="my-project">
                <img class="img-fluid" src="https://fakeimg.pl/250x250" alt>
              </div>
            </swiper-slide>
            <swiper-slide>
              <div class="my-project">
                <img class="img-fluid" src="https://fakeimg.pl/250x250" alt>
              </div>
            </swiper-slide>
            <swiper-slide>
              <div class="my-project">
                <img class="img-fluid" src="https://fakeimg.pl/250x250" alt>
              </div>
            </swiper-slide>

            <div class="swiper-button-prev" slot="button-prev"></div>
            <div class="swiper-button-next" slot="button-next"></div>
          </swiper>

</template>
<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import "swiper/swiper-bundle.min.css";

export default {
  name: "HelloWorld",
  components: { Swiper, SwiperSlide },
  data() {
    return {
      swiperOptions: {
        loop: true,
        autoplay: {
          delay: 2500
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev"
        },
        breakpoints: {
          1: {
            slidesPerView: 1
          },
          768: {
            slidesPerView: 2
          },
          992: {
            slidesPerView: 3
          }
        }
      }
    };
  }
};
</script>
<style>
h4 {
  font-weight: 500;
}

</style>
