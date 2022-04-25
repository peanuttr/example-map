<template>
  <div id="app">
    <MyComponent />
  </div>
</template>

<script>
import MyComponent from "./components/myComponent.vue";

export default {
  
  name: 'App',
  components: {
    MyComponent
  }
}
</script>

<style>
#app {
  height: 100vh;
}
</style>
