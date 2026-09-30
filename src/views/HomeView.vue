<script setup>
  import { ref, onMounted } from 'vue'
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import { Navigation, Pagination, Autoplay, Thumbs, FreeMode } from 'swiper/modules'

  import 'swiper/css'
  import 'swiper/css/navigation'
  import 'swiper/css/pagination'
  import 'swiper/css/free-mode'
  import 'swiper/css/thumbs'

  const thumbsSwiper = ref(null)

  const setThumbsSwiper = (swiper) => {
    thumbsSwiper.value = swiper
  }

  const gallery = Object.values(
    import.meta.glob('@/assets/images/*.jpg', {
      eager: true,
      import: 'default',
    })
  )

  const copyAccount = async (account) => {
    try {
      await navigator.clipboard.writeText(account)
      alert('계좌번호가 복사되었습니다.')
    } catch (error) {
      console.error('복사 실패:', error)
    }
  }
  onMounted(() => {
    const weddingPosition = new naver.maps.LatLng(
      35.8598503,
      127.0956843
    )

    const map = new naver.maps.Map('map', {
      center: weddingPosition,
      zoom: 17
    })

    new naver.maps.Marker({
      position: weddingPosition,
      map: map,
      title: '전주 더메이호텔'
    })
  })

</script>

<template>
  <div class="inner">
    <div class="section-01">
      <img class="main" src="@/assets/images/main.jpg" alt="" />
      <div class="heart-wrap">
        <img class="heart" src="@/assets/images/heart.png" alt="" />
        <div class="text-area">
          <strong>박형석 · 유현지</strong>
          <p>
            2026.11.28 토요일 AM 10:30<br />
            더 메이 호텔 · 마제스틱 볼룸 홀
          </p>
        </div>
      </div>
      <img class="heart-txt" src="@/assets/images/heart-txt.png" alt="" />
    </div>
    <div class="section-02">
      <img src="@/assets/images/letter.jpg" alt="" />
      <div class="letter-area">
        <p>
          저희 두 사람의 만남이<br />
          여름 방학 같았던 8년의 시간이 지나<br />
          사랑의 결실을 맺어<br />
          소중한 결혼식을 올리게 되었습니다.
        </p>
        <p>
          저희 두 사람이 하나 되는 날<br />
          귀한 걸음 하시어<br />
          축복해 주시면 감사하겠습니다.
        </p>
        <ul class="name-list">
          <li>
            <p>박기택 · 이현숙의</p>
            <p>아들</p>
            <p>박형석</p>
          </li>
          <li>
            <p>유기정 · 전유경의</p>
            <p>딸</p>
            <p>유현지</p>
          </li>
        </ul>
      </div>
    </div>
    <div class="section-03">
      <img src="@/assets/images/polaroid.png" alt="" />
    </div>
    <div class="section-04">
      <Swiper
        :thumbs="{ swiper: thumbsSwiper }"
        :modules="[Navigation, Thumbs]"
        class="mySwiper2"
      >
        <SwiperSlide>
          <img src="@/assets/images/img-01.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-02.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-03.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-04.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-05.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-06.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-07.jpg" alt="" />
        </SwiperSlide>
      </Swiper>
      <Swiper
        @swiper="setThumbsSwiper"
        :space-between="10"
        :slides-per-view="4"
        :free-mode="true"
        :watch-slides-progress="true"
        :modules="[Thumbs, FreeMode]"
        class="mySwiper"
      >
        <SwiperSlide>
          <img src="@/assets/images/img-01.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-02.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-03.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-04.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-05.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-06.jpg" alt="" />
        </SwiperSlide>
        <SwiperSlide>
          <img src="@/assets/images/img-07.jpg" alt="" />
        </SwiperSlide>
      </Swiper>
    </div>
    <div class="section-05">
      <div id="map"></div>
    </div>
    <div class="section-06">
      <p>국민 831402-01-101654</p>
      <button @click="copyAccount('국민 831402-01-101654')"></button>
  
    </div>
  </div>
</template>

<style scoped>
#map {
  width: 100%;
  height: 300px;
}
</style>