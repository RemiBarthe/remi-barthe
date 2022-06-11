<template>
  <div>
    <StickyButton style="margin-left: 100px; margin-top: 250px"
      >Ma Value</StickyButton
    >

    <StickyButton>Ma super super Value</StickyButton>
    <img
      alt="ok"
      src="https://dennissnellenberg.com/media/pages/work/emble-studio/cb063dfbe5-1646837261/thumbnail-emble-yellow.jpg"
    />

    <div class="pointers">
      <div
        v-for="pointer in pointers"
        v-show="showPointer"
        class="pointer"
        :style="[pointerPosition, pointerCss(pointer)]"
      ></div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { default as POINTERS, Pointer } from '@/plugins/pointers';

export default defineComponent({
  name: 'HomePage',
  data: () => ({
    mousePointer: {
      x: 0,
      y: 0
    },
    showPointer: false,
    pointers: POINTERS
  }),
  computed: {
    pointerPosition(): string {
      return `transform: translateX(${this.mousePointer.x}px) translateY(${this.mousePointer.y}px);`;
    }
  },
  mounted() {
    document.addEventListener('mousemove', this.onMouseMove);
    document.addEventListener('mouseleave', () => this.hidePointer());
  },
  unmounted() {
    document.removeEventListener('mousemove', this.onMouseMove);
    document.removeEventListener('mouseleave', this.hidePointer());
  },
  methods: {
    onMouseMove(event: MouseEvent) {
      this.showPointer = true;
      this.mousePointer.x = event.pageX - 11;
      this.mousePointer.y = event.pageY - 11;
    },
    pointerCss(pointer: Pointer): string {
      return `
      width: ${pointer.size}px;
      height: ${pointer.size}px;
      transition-duration: ${pointer.transitionDuration}s;
      margin-top: ${pointer.margin}px;
      margin-left: ${pointer.margin}px;
      `;
    },
    hidePointer() {
      setTimeout(() => {
        this.showPointer = false;
      }, 150);
    }
  }
});
</script>

<style lang="scss" scoped>
.pointers {
  .pointer {
    position: absolute;
    top: 0;
    left: 0;
    pointer-events: none;
    will-change: transform;
    border-radius: 50px;
    backface-visibility: hidden;
    background-color: #0a73ba;
    transition: transform cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
}
</style>
