<template>
  <div class="weather-data-container">
    <p class="weather-data">
      {{ Temperature }}: {{ getConvertedTemperature(temperature) }}°{{ isFahrenheit ? 'F' : 'C' }}
    </p>
    <p class="weather-data">
      {{ maxTemperatureDescription }}: {{ getConvertedTemperature(maxTemperature) }}°{{ isFahrenheit ? 'F' : 'C' }}
    </p>
    <p class="weather-data">
      {{ minTemperatureDescription }}: {{ getConvertedTemperature(minTemperature) }}°{{ isFahrenheit ? 'F' : 'C' }}
    </p>
    <p class="weather-data">
      {{ feelsLikeDescription }}: {{ getConvertedTemperature(feelsLike) }}°{{ isFahrenheit ? 'F' : 'C' }}
    </p>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend({
    name: 'TemperatureConverter',
    data() {
      return {
        Temperature: 'temperature',
        maxTemperatureDescription: 'Max temperaure',
        minTemperatureDescription: 'Min temperature',
        feelsLikeDescription: 'feels like'
      }
    },
    props: {
      temperature: {
        type: Number,
        required: true
      },
      maxTemperature: {
        type: Number,
        required: true
      },
      minTemperature: {
        type: Number,
        required: true
      },
      feelsLike: {
        type: Number,
        required: true
      },
      isFahrenheit: {
        type: Boolean,
        required: true
      }
    },
    methods: {
      getConvertedTemperature(value: number): number {
        if (this.isFahrenheit) {
          return this.convertToFahrenheit(value);
        } else {
          return value;
        }
      },
      convertToFahrenheit(celsius: number): number {
        return parseFloat(((celsius * 9 / 5) + 32).toFixed(2));
      },
      handleLanguageChange(newLanguage: string) {
        this.Temperature = newLanguage === 'ru' ? 'temperature' : 'температура',
        this.maxTemperatureDescription = newLanguage === 'ru' ? 'Max temperaure' : 'максимальная температура',
        this.minTemperatureDescription = newLanguage === 'ru' ? 'min temperature' : 'минимальная температура',
        this.feelsLikeDescription = newLanguage === 'ru' ? 'feels like' : 'ощущаемая'
      }
    },
    created() {
      this.$root.$on('languageChanged', this.handleLanguageChange);

      setTimeout(() => {
        const weatherDataElements = document.querySelectorAll('.weather-data');
        weatherDataElements.forEach((element, index) => {
          setTimeout(() => {
            element.classList.add('show');
          }, index * 200); 
        });
      }, 500);
    },
    destroyed() {
      this.$root.$off('languageChanged', this.handleLanguageChange);
    }
  });
</script>

<style scoped lang="scss">
  .weather-data-container {
      display: flex;
      flex-direction: column;
      .weather-data {
        opacity: 0;
        transition: opacity 0.5s;
        margin-top: 1rem;
      }

      .weather-data:nth-child(1) {
        transition-delay: 0s;
      }

      .weather-data:nth-child(2) {
        transition-delay: 0.2s;
      }

      .weather-data:nth-child(3) {
        transition-delay: 0.4s;
      }

      .weather-data:nth-child(4) {
        transition-delay: 0.6s;
      }

      .weather-data.show {
        opacity: 1;
      }
    }
</style>

