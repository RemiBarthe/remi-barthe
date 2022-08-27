<template>
  <div
    ref="backgroundForm"
    class="form-container"
    @mousemove="formMove"
    @mouseleave="formHover = false"
    :style="formPosition"
  >
    <!-- <div class="background"></div> -->

    <img
      style="margin-top: 600px; margin-left: 900px"
      alt="ojk"
      src="../assets/images/atom.png"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'BackgroundForm',
  data: () => ({
    formX: 0,
    formY: 0,
    formHover: false
  }),
  computed: {
    formPosition(): string {
      if (this.formHover)
        return `transform: translateX(${this.formX}px) translateY(${this.formY}px);`;

      return '';
    }
  },
  methods: {
    formMove(event: MouseEvent) {
      const formPosition = {
        width: this.$refs.backgroundForm.clientWidth,
        height: this.$refs.backgroundForm.clientHeight,
        left: this.$refs.backgroundForm.getBoundingClientRect().left,
        top: this.$refs.backgroundForm.getBoundingClientRect().top
      };

      this.formHover = true;
      this.formX = (event.x - formPosition.left - formPosition.width / 2) / 5;
      this.formY = (event.y - formPosition.top - formPosition.height / 2) / 5;
    }
  }
});
</script>

<style lang="scss" scoped>
.form-container {
  width: 200px;
  height: 200px;
  transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.8s;
  display: flex;
  position: relative;
  align-items: center;
  justify-content: center;
  will-change: transform;
  z-index: 11;

  .background {
    background-color: #4062bb;
    position: absolute;
    border-radius: 12px;
    will-change: transform;
    width: 165px;
    height: 165px;
    z-index: 9;
  }
}
</style>
