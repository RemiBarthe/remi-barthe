<template>
  <button><slot></slot></button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'StickyButton',
  data: () => ({})
});
</script>
