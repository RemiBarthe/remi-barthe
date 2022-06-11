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
      // console.log('###################');
      // console.log('client =>', event.clientX - this.buttonWidth, event.clientY);
      // console.log('page =>', event.pageX - this.buttonWidth, event.pageY);
      // console.log('screen =>', event.screenX - this.buttonWidth, event.screenY);
      // console.log('xy =>', event.x - this.buttonWidth, event.y);
      // console.log(this.$refs.stickyButton.getBoundingClientRect().left);
      // console.log(this.$refs.stickyButton.getBoundingClientRect().top);

      // console.log('###################');

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

  .sticky-button {
    padding: 20px 40px;
    border: none;
    z-index: 10;
    background-color: transparent;
    // border: solid 3px violet;
    will-change: transform;
  }
  .button-background {
    background-color: white;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.3s;
    position: absolute;
    border-radius: 12px;
    will-change: transform;
    width: 0%;
    height: 20%;
  }
  &:hover {
    z-index: 11;
    .sticky-button {
      color: white;
    }

    .button-background {
      background-color: #0a73ba;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
