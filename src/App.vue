<template>
  <div id="app" :class="{ 'newTheme': newTheme }">
    <Header />
    <div class="navbar">
      <Translate />
      <Search @search="fetchData" />
      <ThemeToggle />
    </div>
    <WeatherBox :weatherData="weatherData" v-if="weatherData" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Search from './components/Search.vue';
import WeatherBox from './components/WeatherBox.vue'
import Translate from './components/Translate.vue';
import Header from './components/Header.vue'
import ThemeToggle from './components/ThemeToggle.vue';

export default Vue.extend({
  name: 'App',
  components: {
    Search,
    WeatherBox,
    Translate,
    Header,
    ThemeToggle
  },
  data() {
    return {
      weatherData: null,
      api_base: 'https://api.openweathermap.org/data/2.5/weather?',
      api_key: '64b8a681c642a6c8ed92a2f3fa49c268',
      newTheme: false
    };
  },
  created() {
    this.$root.$on('theme-changed', this.handleThemeChange);
  },
  destroyed() {
    this.$root.$off('theme-changed', this.handleThemeChange);
  },
  methods: {
    fetchData(search: string) {
      fetch(`${this.api_base}q=${search}&appid=${this.api_key}`)
        .then(res => res.json())
        .then(data => {
          this.weatherData = data
          console.log(data)
        })
    },
    handleThemeChange(newTheme: boolean) {
      this.newTheme = newTheme;
    }
  },
  watch: {
    
  }
});
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    text-transform: uppercase;
  }

  #app {
    background-color: rgb(180, 90, 16);
    min-height: 100vh;
    color: rgb(221, 219, 219);
    text-align: center;
    padding: 1rem .7rem;
  }

  .newTheme {
    background-color: #333 !important;
  }

  .navbar {
    display: flex;
    justify-content: space-between;
    padding: 0 1rem 0;
    align-items: center;
  }

  @media only screen and (min-width: 1024px) {
    .navbar {
      display: flex;
      justify-content: space-evenly;
    }
  }
</style>
