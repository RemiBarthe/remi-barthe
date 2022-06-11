<template>
  <div>
    <StickyButton>Ma Value</StickyButton>

    <div class="pointers">
      <div
        v-for="pointer in pointers"
        class="pointer"
        :style="[pointerPosition, pointerCss(pointer)]"
      ></div>
      <!-- <div class="pointer" :style="pointerPosition"></div>
      <div class="pointer" :style="pointerPosition"></div>
      <div class="pointer" :style="pointerPosition"></div>
      <div class="pointer" :style="pointerPosition"></div>
      <div class="pointer" :style="pointerPosition"></div> -->
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface Pointer {
  size: Number;
  transitionDuration: Number;
  margin: Number;
}

export default defineComponent({
  name: 'HomePage',
  data: () => ({
    mousePointer: {
      x: 0,
      y: 0
    },
    pointers: [
      {
        size: 18,
        transitionDuration: 0.34,
        margin: 0
      } as Pointer,
      {
        size: 17,
        transitionDuration: 0.32,
        margin: 0.5
      } as Pointer,
      {
        size: 16,
        transitionDuration: 0.3,
        margin: 1
      } as Pointer,
      {
        size: 15,
        transitionDuration: 0.28,
        margin: 1.5
      } as Pointer,
      {
        size: 14,
        transitionDuration: 0.26,
        margin: 2
      } as Pointer,
      {
        size: 13,
        transitionDuration: 0.24,
        margin: 2.5
      } as Pointer,
      {
        size: 10,
        transitionDuration: 0.22,
        margin: 4
      } as Pointer
    ]
  }),
  computed: {
    pointerPosition() {
      return `transform: translateX(${this.mousePointer.x}px) translateY(${this.mousePointer.y}px);`;
    }
  },
  mounted() {
    document.addEventListener('mousemove', this.onMouseMove);
  },
  unmounted() {
    document.removeEventListener('mousemove', this.onMouseMove);
  },
  methods: {
    onMouseMove(event: MouseEvent) {
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
