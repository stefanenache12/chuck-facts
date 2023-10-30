<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import MainComponent from "./components/MainComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    MainComponent,
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<template>
  <HeaderComponent/>

  <MainComponent />
</template>

<style lang="scss">
@use "assets/scss/main";
</style>
