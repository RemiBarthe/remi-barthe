<template>
  <div
    ref="stickyButton"
    class="button-container"
    @mousemove="buttonMove"
    @mouseleave="buttonHover = false"
    :style="buttonPosition"
  >
    <div class="button-background"></div>

    <button class="sticky-button" :style="buttonPosition"><slot></slot></button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'StickyButton',
  data: () => ({
    buttonX: 0,
    buttonY: 0,
    buttonHover: false
  }),
  computed: {
    buttonPosition(): string {
      if (this.buttonHover)
        return `transform: translateX(${this.buttonX}px) translateY(${this.buttonY}px);`;

      return '';
    }
  },
  methods: {
    buttonMove(event: MouseEvent) {
      const buttonPosition = {
        width: this.$refs.stickyButton.clientWidth,
        height: this.$refs.stickyButton.clientHeight,
        left: this.$refs.stickyButton.getBoundingClientRect().left,
        top: this.$refs.stickyButton.getBoundingClientRect().top
      };

      this.buttonHover = true;
      this.buttonX =
        (event.x - buttonPosition.left - buttonPosition.width / 2) / 7;
      this.buttonY =
        (event.y - buttonPosition.top - buttonPosition.height / 2) / 7;
    }
  }
});
</script>

<style lang="scss" scoped>
.button-container {
  width: fit-content;
  transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.1s;
  display: flex;
  position: relative;
  align-items: center;
  justify-content: center;
  will-change: transform;
  // z-index: 11;

  .sticky-button {
    padding: 10px;
    border: none;
    z-index: 10;
    background-color: transparent;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.2s;
    // border: solid 3px violet;
    will-change: transform;
  }
  .button-background {
    background-color: transparent;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.4s;
    position: absolute;
    border-radius: 18px;
    will-change: transform;
    width: 0%;
    height: 20%;
    z-index: 9;
  }

  &:hover {
    .sticky-button {
      color: white;

      filter: invert(100%);
    }

    .button-background {
      background-color: #4062bb;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
