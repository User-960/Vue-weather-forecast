<script>
  export default {
    data: () => ({
      city: "",
      error: ""
    }),
    methods: {
      getWeather() {
        if (this.city.trim().length < 2) {
          this.error = "More than one character required";
          return false;
        }
        this.error = "";
      }
    },
    computed: {
      cityName() {
        return "«" + this.city + "»";
      }
    }
  }
</script>

<template>
  <div class="container pt-5">
    <div class="weather__inner card">
      <h1 class="weather__title">Weather Forecast</h1>
      <p class="weather__text">Check the weather in {{ city == "" ? "your city" : cityName }}</p>
      <input class="weather__input" v-model="city" type="text" placeholder="Enter city">
      <button class="weather__btn btn primary" v-if="city != ''" @click="getWeather()">Get weather</button>
      <button disabled class="weather__btn btn primary" v-else>Enter the name of the city</button>
      <p class="weather__error">{{ error }}</p>
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

.weather__input {
  margin-top: 30px;
  display: inline-block;
}

.weather__btn {
  margin-left: 20px;
}

.weather__error {
  color: #e53935;
}
</style>
