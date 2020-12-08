<template>
  <div>
    <swiper :options="swiperOption">
      <swiper-slide>スライダー１</swiper-slide>
      <swiper-slide>スライダー２</swiper-slide>
      <swiper-slide>スライダー３</swiper-slide>
   
    <div slot="pagination" class="swiper-pagination" />
    <div slot="button-prev" class="swiper-button-prev" />
    <div slot="button-next" class="swiper-button-next" />
     </swiper>
  </div>
</template>

<script>
export default {
  data() {
    return {
      swiperOption: {
        speed: 1000, //スライドの切り替わりスピード
        spaceBetween: 30, //各スライドの余白
        centeredSlides: true, //スライダーを真ん中に
        loop: true, //無限ループ
        autoplay: {
          //スライドの自動切り替え
          delay: 5000, //スライドの自動切り替えの秒数
          disableOnInteraction: false, //何らかのアクション後の自動切り替えを再開
        },
        pagination: {
          //ページネーション設定
          el: ".swiper-pagination",
          clickable: true,
        },
        navigation: {
          //ナビゲーション設定
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
      },
    };
  },
};
</script>