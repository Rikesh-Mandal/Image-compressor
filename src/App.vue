<template>
  <div id="app">
    <ImageCompressor />
  </div>
</template>

<script>
import ImageCompressor from './components/ImageCompressor.vue';

export default {
  name: 'App',
  components: {
    ImageCompressor,
  },
};
</script>

<style>
#app {
  text-align: center;
  padding: 20px;
}
</style>
