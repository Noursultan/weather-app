<template>
    <div>
        <h2>{{ headerText }}</h2>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue';

    export default Vue.extend({
        name: 'HeaderComponent',
        data () {
            return {
                headerText: 'Weather App'
            }
        },
        created() {
            this.$root.$on('languageChanged', this.handleLanguageChange);
        },
        destroyed() {
            this.$root.$off('languageChanged', this.handleLanguageChange);
        },
        methods: {
            handleLanguageChange(newLanguage: string) {
                this.headerText = newLanguage === 'ru' ? 'weather app' : '"погода"';
            }
        }
    });
</script>

<style scoped lang="scss">
 h2 {
    margin-bottom: 1rem;
 }

 @media only screen and (min-width: 1024px) {
    h2 {
        margin-bottom: 2rem;
    }
  }
</style>