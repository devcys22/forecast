<script setup>
import { useWeatherStore } from '@/stores/weather';
import { storeToRefs } from 'pinia';
import {  onBeforeMount } from 'vue';
import dayjs from 'dayjs';
import {getImage} from '@/composables/helper.js'

onBeforeMount(() => {
  weatherStore.getCityName(); 
  weatherStore.getCurrentWeatherInfo();
})

//서울 날씨 정보를 요청하는 API
const weatherStore = useWeatherStore();
const {currentConditions, address} = storeToRefs(weatherStore);


</script>

<template>
  <header v-if="currentConditions" class="header">
      <!-- 지역 -->
      <h1 class="header__title">
        <span class="material-symbols-outlined"> location_on </span>{{address}}
      </h1>
      <h2 class="header__date">{{ dayjs().format('HH:mm') }}</h2>
    </header>
    <!-- 현재 날씨 -->
    <main v-if="currentConditions" class="main">
      <article class="weather">
        <section class="weather__info">
          <img
            :src="getImage(currentConditions.icon)"
            :alt="`${currentConditions.datetime} ${currentConditions.temp}`"
            class="weather__img"
          />
          <h3 class="weather_temp">{{currentConditions.temp}}</h3>
          <p class="weather_summary">{{ currentConditions.conditions }}</p>
          <ul class="weather__moreList">
            <li class="weather__moreListItem">
              <p class="weather__subtitle">습도</p>
              <p class="weather__desc">{{currentConditions.humidity}}</p>
            </li>
            <li class="weather__moreListItem">
              <p class="weather__subtitle">풍속</p>
              <p class="weather__desc">{{ currentConditions.windspeed }}</p>
            </li>
            <li class="weather__moreListItem">
              <p class="weather__subtitle">체감</p>
              <p class="weather__desc">{{currentConditions.feelslike}}</p>
            </li>
          </ul>
        </section>
      </article>
    </main>
</template>
