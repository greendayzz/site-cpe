<template>
  <div id="app">
    <app-map></app-map>
  </div>
</template>
<script>
import AppMap from "./components/AppMap.vue";
export default {
  components: {
    AppMap,
  },
};
</script>
<style>
html,body{
  margin: 0;
  padding: 0;
}
#app{
  position: fixed;
  width: 100%;
  height: 100%;
}
</style>
