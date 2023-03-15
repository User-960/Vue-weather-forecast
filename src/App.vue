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
          .then(res => (this.info = res.data));

        this.city = "";
      },
      getNameCity() {
        if (this.city !== "") {
          this.getWeather();
          this.city = "";
        }
      }
    },
    computed: {
      cityName() {
        return "«" + this.city + "»";
      },
      showCity() {
        return this.info.name;
      },
      showCoords() {
        return `https://yandex.ru/maps/?pt=${this.info.coord.lon},${this.info.coord.lat}&z=10&l=map`;
      },
      showImg() {
        return "http://openweathermap.org/img/wn/" + this.info.weather[0].icon + ".png";
      },
      showImgAlt() {
        return this.info.weather[0].description;
      },
      showState() {
        return this.info.weather[0].main;
      },
      showTemp() {
        return Math.round(this.info.main.temp) + " °C";
      },
      showFeelsLike() {
        return "Feels like: " + Math.round(this.info.main.feels_like) + " °C";
      },
      showMinTemp() {
        return Math.round(this.info.main.temp_min) + " °C";
      },
      showMaxTemp() {
        return Math.round(this.info.main.temp_max) + " °C";
      }
    }
  }
</script>

<template>
  <div class="container pt-2">
    <div class="weather__inner card">
      <h1 class="weather__title">Weather Forecast</h1>
      <p class="weather__text">Check the weather in {{ city == "" ? "your city" : cityName }}</p>
      <input class="weather__input" v-model="city" type="text" v-on:keypress.enter="getNameCity" placeholder="Enter city">
      <button class="weather__btn btn primary" v-if="city != ''" @click="getWeather()">Get weather</button>
      <button disabled class="weather__btn btn primary" v-else>Enter city</button>
      <p class="weather__error">{{ error }}</p>

      <div class="weather__info" v-if="info != null">
        <a class="weather__info-link" :href="showCoords">
          <span>{{ showCity }}</span>
          <img class="weather__info-img" src="./assets/images/marker.svg" alt="marker">
        </a>
        <div class="weather__info-block">
          <img :src="showImg" :alt="showImgAlt">
          <p class="weather__info-block-temp">{{ showTemp }}</p>
        </div>
        <div class="weather__info-block-minmax">
          <p>{{ showMaxTemp }} / {{ showMinTemp }} | {{ showFeelsLike }}</p>
        </div>
        <span>{{ showState }}</span>
      </div>
      
    </div>
  </div>
</template>

<style scoped>
.weather__inner {
  height: 100%;
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
  margin-bottom: 15px;
}

.weather__btn {
  margin-left: 20px;
}

.weather__error {
  color: #e53935;
}

.weather__info {
  padding: 20px;
  max-height: 280px;
  max-width: 500px;
  margin: 0 auto;
  color: #fff;
  border-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: rgb(69,72,151);
  background: linear-gradient(180deg, rgb(92, 95, 182) 0%, rgb(86, 123, 171) 35%, rgba(58,157,178,1) 100%);
}

.weather__info-link {
  color: #fff;
  font-weight: 800;
  font-size: 18px;
}

.weather__info-block {
  display: flex;
  justify-content: center;
  height: 80px;
}

.weather__info-block img {
  height: 45px;
  align-self: center;
}

.weather__info-block-temp {
  margin: 0;
  margin-left: 10px;
  align-self: center;
  font-size: 30px;
}

.weather__info-img {
  margin-left: 5px;
  width: 18px;
  height: 18px;
}
</style>
