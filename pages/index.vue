<template>
  <div>
    <StickyButton>Ma Value</StickyButton>

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
    pointerPosition() {
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
      this.mousePointer.x = event.pageX - 18;
      this.mousePointer.y = event.pageY - 42;
    },
    pointerCss(pointer: Pointer) {
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
    pointer-events: none;
    will-change: transform;
    border-radius: 50px;
    backface-visibility: hidden;
    background-color: blue;
    transition: transform cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
}
</style>
