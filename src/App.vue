<script>
  import axios from "axios";

  export default {
    data: () => ({
      city: "",
      error: "",
      info: null
    }),
    methods: {
      getWeather() {
        if (this.city.trim().length < 2) {
          this.error = "More than one character required";
          return false;
        }
        this.error = "";

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=b178e36737a1b78abd26914eec95656d`)
          .then(res => (this.info = res.data))
      }
    },
    computed: {
      cityName() {
        return "«" + this.city + "»";
      },
      showTemp() {
        return "Temperature: " + this.info.main.temp;
      },
      showFeelsLike() {
        return "Feels like: " + this.info.main.feels_like;
      },
      showMinTemp() {
        return "Minimum temperature: " + this.info.main.temp_min;
      },
      showMaxTemp() {
        return "Maximum temperature: " + this.info.main.temp_max;
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

      <p v-show="info != null">{{ info }}</p>
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
