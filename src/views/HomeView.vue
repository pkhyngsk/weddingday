<script setup>
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import { onMounted } from 'vue'

  import 'swiper/css'
  import 'swiper/css/navigation'
  import 'swiper/css/pagination'

  import { Navigation, Pagination, Autoplay } from 'swiper/modules'

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
      <img class="info" src="@/assets/images/info.png" alt="" />
      <img class="info-title" src="@/assets/images/info-title.png" alt="" />
      <div class="dim"></div>
    </div>
    <div class="section-02">
      <!-- <p>
        저희 두 사람의 만남이<br />
        여름 방학 같았던 8년의 시간이 지나<br />
        사랑의 결실을 맺어<br />
        소중한 결혼식을 올리게 되었습니다.<br />
        <br />
        저희 두 사람이 하나 되는 날<br />
        귀한 걸음 하시어<br />
        축복해 주시면 감사하겠습니다.
      </p> -->
      <img class="letter" src="@/assets/images/letter.png" alt="" />
    </div>
    <div class="section-03">
      <p><span>박기택 · 이현숙</span> 의 장남 <span>박형석</span></p>
      <p><span>유기정 · 전유경</span> 의 장녀 <span>유현지</span></p>
    </div>
    <div class="section-04">
      <Swiper
      :modules="[Pagination, Autoplay]"
      :slides-per-view="1"
      :loop="true"
      :speed=1500
      :autoplay="{
        delay: 3000,
        disableOnInteraction: false,
      }"
      :pagination="{
        type: 'fraction',
        formatFractionCurrent: (number) => String(number).padStart(2, '0'),
        formatFractionTotal: (number) => String(number).padStart(2, '0'),
      }"
    >
      <SwiperSlide v-for="(item, index) in gallery" :key="index">
        <img :src="item" alt="" />
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