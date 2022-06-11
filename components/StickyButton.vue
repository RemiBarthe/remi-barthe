<template>
  <div
    ref="stickyButton"
    class="button-container"
    @mousemove="buttonMove"
    @mouseleave="buttonHover = false"
    :style="buttonPosition"
  >
    <div class="button-background"></div>

    <button class="sticky-button" :style="textPosition"><slot></slot></button>
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
    },
    textPosition(): string {
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
        (event.x - buttonPosition.left - buttonPosition.width / 2) / 4;
      this.buttonY =
        (event.y - buttonPosition.top - buttonPosition.height / 2) / 4;
    }
  }
});
</script>

<style lang="scss" scoped>
.button-container {
  width: fit-content;
  transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.3s;
  display: flex;
  position: relative;

  .sticky-button {
    padding: 20px;
    border: none;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.3s;
    z-index: 10;
    background-color: transparent;
  }
  &:hover {
    .sticky-button {
      color: white;
    }

    .button-background {
      background-color: blue;
    }
  }

  .button-background {
    width: 100%;
    height: 100%;
    background-color: white;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.2s;
    position: absolute;
  }
}
</style>
