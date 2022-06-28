<template>
  <div class="animated-bar">
    <div v-for="i in 12"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'AnimatedBar'
});
</script>

<style lang="scss" scoped>
.animated-bar {
  width: 30px;
  height: 140px;
  margin-right: 40px;
  overflow: hidden;

  div {
    width: 80px;
    height: 7px;
    background-color: #4062bb;
    margin-bottom: 10px;
    animation: slide 1.8s linear infinite;
  }
}
</style>
