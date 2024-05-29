<template>
  <div id="app">
    <ThreeScene />
  </div>
</template>

<script>
import ThreeScene from './components/model.vue';

export default {
  components: {
    ThreeScene,
  },
};
</script>
<style>
.webgl {
  position: absolute;
  top: 0;
  left: 0;
}
</style>