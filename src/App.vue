<template>
  <Index />
</template>

<script>

import Index from './view/index.vue';

export default {
  name: 'App',
  components: { Index }
}
</script>

<style>
  * {
    padding: 0;
    margin: 0;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
		height: 90vh;
		width: 90vw;
  }
</style>
