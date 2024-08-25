<script setup>
import { useWeatherStore } from '@/stores/weather';
import { storeToRefs } from 'pinia';
import {  onBeforeMount } from 'vue';
import dayjs from 'dayjs';
import {getImage} from '@/composables/helper.js'
//서울 날씨 정보를 요청하는 API
const weatherStore = useWeatherStore();
const {hours} = storeToRefs(weatherStore);
onBeforeMount(() => {
    weatherStore.getCurrentWeatherInfo();
})

</script>

<template>
  <article class="forecast">
      <!-- 시간별 예보 -->
      <section class="forecast__today">
        <strong class="forecast__title">시간별</strong>
        <ul class="week__list">
          <!-- 시간별 예보 상세 아이템 -->
          <li v-for="hour in hours" :key="hour.datetime" class="week__list__item">
            <span>{{dayjs(`2024-07-01 ${hour.datetime}`).format('H')}}</span>
            <!-- todo 23시 이후데이터 안보임 확인하고 수정해보기 -->
            <img :src="getImage(hour.icon)" 
                  :alt="`{hour.datetime} ${hour.temp}도`" class="week_icons" />
            <span>{{ hour.temp }}</span>
          </li>
        </ul>
      </section>
      <!-- 중기 예보 -->
      <section class="forecast__week">
        <strong class="forecast__title">중기예보</strong>
        <ul class="forecast__weekList">
          <!-- 중기 예보 상세 아이템 -->
          <li class="forecast__weekListItem">
            <div class="forecast__itemLeft">
              <strong class="forecast__day">월요일</strong>
              <span class="forecast__date">2024.07.01</span>
            </div>
            <div class="forecast__itemMiddle">
              <strong class="forecast__tmp">32°</strong>
            </div>
            <div class="forecast__itemRight">
              <img
                src="@/assets/images/icons/hail.png"
                alt=""
                class="forecast__weekListImg"
              />
            </div>
          </li>
        </ul>
      </section>
    </article>
</template>
