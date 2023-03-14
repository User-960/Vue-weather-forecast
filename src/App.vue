<script></script>

<template>
  <div class="container pt-5">
    <div class="weather__inner card">
      <h1 class="weather__title">Weather Forecast</h1>
      <p class="weather__text">Check the weather in your city</p>
      <input class="weather__input" type="text" placeholder="Enter city">
      <button class="btn primary">Get weather</button>
    </div>
  </div>
</template>

<style scoped>
.weather__inner {
  height: 500px;
  padding: 20px;
  text-align: center;
  color: #000;
}

.weather__title {
  margin-top: 50px;
}

.weather__text {
  margin-top: 20px;
}
</style>
