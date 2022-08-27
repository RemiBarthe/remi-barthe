<template>
  <div class="links">
    <StickyButton>
      <img alt="logo github" src="../assets/images/github.svg" />
    </StickyButton>

    <StickyButton>
      <img alt="logo at mail" src="../assets/images/at.svg" />
    </StickyButton>

    <StickyButton>
      <img alt="logo linkedin" src="../assets/images/linkedin.svg" />
    </StickyButton>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'LinkBlock'
});
</script>

<style lang="scss" scoped>
.links {
  display: flex;
  transform: rotate(5.45deg);
  cursor: pointer;
}
</style>
