<template>
  <div class="wrapper">
    <input 
      type="text" 
      v-model="query" 
      @keyup.enter="saveInput" 
      :placeholder="placeholderDescription" 
      :class="{ 'hovered': isButtonHovered }"
    >
    <button 
      @click="saveInput" 
      @mouseover="isButtonHovered = true" 
      @mouseout="isButtonHovered = false"
    >
      {{ search }}
    </button>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend({
    name: 'SearchComponent',
    data() {
      return {
        query: '',
        placeholderDescription: 'type any city...',
        search: 'search',
        isButtonHovered: false
      }
    },
    created() {
      this.$root.$on('languageChanged', this.handleLanguageChange);
    },
    destroyed() {
      this.$root.$off('languageChanged', this.handleLanguageChange);
    },
    methods: {
      saveInput: function() {
        this.$emit('search', this.query)
        this.query = ''
      },
      handleLanguageChange(newLanguage: string) {
        this.placeholderDescription = newLanguage === 'ru' ? 'type any city...' : 'введите город...';
        this.search = newLanguage === 'ru' ? 'search' : 'искать';
      }
    }
  });
</script>

<style scoped lang="scss">
  .wrapper {
    position: relative;

    input {
      padding: .8rem 2.5rem .8rem .8rem;
      border-radius: 3rem;
      border: none;
      outline: none;
      &:valid {
        color: rgb(113, 109, 109);
      }
      &::placeholder {
        text-transform: capitalize;
      }
    }

    button {
      position: absolute;
      background-color: rgb(86, 84, 84);
      top: .1rem;
      right: .1rem;
      padding: .7rem;
      border-radius: 3rem;
      border: none;
      color: rgb(255, 255, 255);
      text-transform: capitalize;
      transition: background-color 0.3s, color 0.3s;
      cursor: pointer;
      margin-left: .1rem;
      &:hover {
          background-color: white;
          color: rgb(113, 109, 109);
      }
    }
    .hovered {
      background-color: rgb(186, 179, 179);
    }
  }
</style>
