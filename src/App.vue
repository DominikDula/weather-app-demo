<template>
  <div id="app">
    <MainScreen/>
  </div>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";

export default {
  name: "App",
  components: {
    MainScreen
  }
};
</script>

<style src="@/assets/scss/main.scss" lang="scss"></style>
