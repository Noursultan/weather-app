<template>
    <div>
        <button @click="toggleLanguage">{{ language === 'ru' ? 'русский' : 'english' }}</button>
    </div>
</template>
  
<script lang="ts">
  import Vue from 'vue';
  
  export default Vue.extend({
    name: 'TranslateComponent',
    data () {
        return {
            language: 'ru'
        }
    },
    methods: {
        toggleLanguage() {
            this.language = this.language === 'ru' ? 'en' : 'ru';
            this.$root.$emit('languageChanged', this.language); 
        },
    },
  });
</script>
  
<style scoped lang="scss">
    button {
        padding: .7rem;
        border-radius: 3rem;
        border: none;
        color: rgb(113, 109, 109);
        transition: background-color 0.3s, color 0.3s;
        cursor: pointer;
        text-transform: capitalize;
        &:hover {
            background-color: rgb(86, 84, 84);
            color: rgb(255, 255, 255);
        }
    }
</style>