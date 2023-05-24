<template>
    <div>
        <h2>{{ weatherData.name }}</h2>
        <button @click="toggleTemperatureUnit">{{ tempSwitch }}</button>
        <TemperatureConverter 
            :temperature="weatherData.main.temp" 
            :isFahrenheit="isFahrenheit" 
            :maxTemperature="weatherData.main.temp_max"
            :minTemperature="weatherData.main.temp_min"
            :feelsLike="weatherData.main.feels_like"
        />
        <div class="weather-data-container">
          <p class="weather-data">{{ humidity }}: {{ weatherData.main.humidity }}%</p>
          <p class="weather-data">{{ pressure }}: {{ weatherData.main.pressure }}%</p>
          <p class="weather-data">{{ windSpeed }}: {{ weatherData.wind.speed }} {{ meterSec }}</p>
          <p class="weather-data">{{ windDegree }}: {{ weatherData.wind.deg }}°</p>
        </div>
    </div>
</template>
  
<script lang="ts">
  import Vue from 'vue';
  import TemperatureConverter from './TemperatureConverter.vue';
  
  export default Vue.extend({
    name: 'WeatherBox',
    props: {
      weatherData: {
        type: Object,
        required: true
      }
    },
    components: {
      TemperatureConverter
    },
    data() {
      return {
        isFahrenheit: false,
        tempSwitch: 'Switch Temp Unit',
        humidity: 'humidiy',
        pressure: 'pressure',
        windSpeed: 'wind speed',
        windDegree: 'wind degreee',
        meterSec: 'meter/sec',
      };
    },
    methods: {
      toggleTemperatureUnit() {
        this.isFahrenheit = !this.isFahrenheit;
      },
      handleLanguageChange(newLanguage: string) {
        this.tempSwitch = newLanguage === 'ru' ? 'Switch Temp Unit' : 'Поменять измерение температуры';
        this.humidity = newLanguage === 'ru' ? 'humidiy' : 'влажность';
        this.pressure = newLanguage === 'ru' ? 'pressure' : 'давление';
        this.windSpeed = newLanguage === 'ru' ? 'Wind Speed' : 'скорость ветра';
        this.windDegree = newLanguage === 'ru' ? 'wind degree' : 'направление ветра'
        this.meterSec = newLanguage === 'ru' ? 'meter/sec' : 'метров/сек'
      },
      // animateWeatherData() {
      //   setTimeout(() => {
      //     const weatherDataElements = document.querySelectorAll('.weather-data');
      //     weatherDataElements.forEach((element, index) => {
      //       setTimeout(() => {
      //         element.classList.add('show');
      //       }, (index * 200)); 
      //     });
      //   }, 500);
      // }
    },
    created() {
      this.$root.$on('languageChanged', this.handleLanguageChange);

      setTimeout(() => {
        const weatherDataElements = document.querySelectorAll('.weather-data');
        weatherDataElements.forEach((element, index) => {
          setTimeout(() => {
            element.classList.add('show');
          }, (index * 200)); 
        });
      }, 500);
    },
    destroyed() {
      this.$root.$off('languageChanged', this.handleLanguageChange);
    }
  });
</script>
  
<style scoped lang="scss">
    h2, button, p {
        margin-top: 1rem;
    }
    button {
        cursor: pointer;
        border-radius: 3rem;
        border: none;
        padding: .5rem;
        font-size: .7rem;
        color: rgb(113, 109, 109);
        transition: background-color 0.3s, color 0.3s;
        &:hover {
            background-color: rgb(86, 84, 84);
            color: rgb(255, 255, 255);
        }
    }
    .weather-data-container {
      display: flex;
      flex-direction: column;
      .weather-data {
        opacity: 0;
        transition: opacity 0.5s;
      }

      .weather-data:nth-child(1) {
        transition-delay: 1.2s;
      }

      .weather-data:nth-child(2) {
        transition-delay: 1.4s;
      }

      .weather-data:nth-child(3) {
        transition-delay: 1.6s;
      }

      .weather-data:nth-child(4) {
        transition-delay: 1.8s;
      }

      .weather-data.show {
        opacity: 1;
      }
    }
</style>
  