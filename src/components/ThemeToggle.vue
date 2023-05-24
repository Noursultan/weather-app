<template>
    <button class="theme-toggle" @click="toggleTheme">
        <span class="toggle-icon" :class="{ 'active': isLightTheme }"></span>
  </button>
</template>

<script lang="ts">
    import Vue from 'vue';

    export default Vue.extend({
        name: 'ThemeToggle',
        data() {
            return {
                isLightTheme: false
            };
        },
        methods: {
            toggleTheme() {
                this.isLightTheme = !this.isLightTheme;
                this.$root.$emit('theme-changed', this.isLightTheme);
            }
        }
    });
</script>

<style scoped lang="scss">
    .theme-toggle {
        padding: 0;
        border: none;
        background: none;
        cursor: pointer;
    }

    .toggle-icon {
        display: inline-block;
        width: 35px;
        height: 35px;
        background-color: #333;
        border-radius: 50%;
        transition: background-color 0.3s;
        vertical-align: middle;
    }

    .toggle-icon.active {
        background-color: #f2f2f2;
    }
</style>