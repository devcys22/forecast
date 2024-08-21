<script setup>
import { onBeforeMount } from 'vue';
import axios from 'axios';
onBeforeMount(async() => {
  //서울 날씨 정보를 요청하는 API
  const result = await axios.get('https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/seoul?key=ZY7EJFHJCGKS83TZJLQGJDHG2&uniGroup=metric&lang=ko');
  console.log(result);
});
</script>

<template>
  <header class="header">
      <!-- 지역 -->
      <h1 class="header__title">
        <span class="material-symbols-outlined"> location_on </span>서울
      </h1>
      <h2 class="header__date">11:00</h2>
    </header>
    <!-- 현재 날씨 -->
    <main class="main">
      <article class="weather">
        <section class="weather__info">
          <img
            src="@/assets/images/icons/cloudy.png"
            alt=""
            class="weather__img"
          />
          <h3 class="weather_temp">28°</h3>
          <p class="weather_summary">대체로 맑음</p>
          <ul class="weather__moreList">
            <li class="weather__moreListItem">
              <p class="weather__subtitle">습도</p>
              <p class="weather__desc">82%</p>
            </li>
            <li class="weather__moreListItem">
              <p class="weather__subtitle">풍속</p>
              <p class="weather__desc">4.12/ms</p>
            </li>
            <li class="weather__moreListItem">
              <p class="weather__subtitle">체감</p>
              <p class="weather__desc">7도</p>
            </li>
          </ul>
        </section>
      </article>
    </main>
</template>
