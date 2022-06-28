<template>
  <div class="page-container">
    <div class="page-header">
      <h1 class="name-title">Rémi Barthe</h1>

      <LinkBlock />
    </div>

    <div class="presentation">
      <div class="title">
        <AnimatedBar />

        <h2>
          web_ <br />
          developer
        </h2>
      </div>

      <h3 class="subtitle">Lorem ipsum sit amet dolor loprem alork</h3>
    </div>

    <div>Hello</div>
    <!-- <div class="pointers">
      <div
        v-for="pointer in pointers"
        v-show="showPointer"
        class="pointer"
        :style="[pointerPosition, pointerCss(pointer)]"
      ></div>

      <BackgroundForm />
    </div>

    <svg>
      <defs>
        <filter id="filter">
          <feGaussianBlur in="SourceGraphic" stdDeviation="8" result="blur" />
          <feColorMatrix
            in="blur"
            mode="matrix"
            values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 28 -10"
            result="filter"
          />
          <feComposite in="SourceGraphic" in2="filter" operator="atop" />
        </filter>
      </defs>
    </svg> -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { default as POINTERS, Pointer } from '@/plugins/pointers';
import '@/assets/style/global.scss';
import '@/assets/style/animation.scss';

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
      transition-duration: ${pointer.transitionDuration * 2}s;
      margin-top: ${pointer.margin}px;
      margin-left: ${pointer.margin}px;
      `;
    },
    hidePointer() {
      setTimeout(() => {
        this.showPointer = false;
      }, 250);
    }
  }
});
</script>

<style lang="scss" scoped>
.page-container {
  padding: 20px 80px;
  height: calc(100vh - 40px);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  .page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    .name-title {
      font-size: 1.5rem;
      font-family: 'ZenKakuBlack';
    }
  }
  .presentation {
    display: flex;
    flex-flow: column wrap;
    align-content: flex-start;
    align-items: flex-end;
    padding: 0 80px;

    .title {
      font-size: 6rem;
      font-family: 'LeagueSpartan';
      display: flex;
      align-items: center;

      h2 {
        margin: 0;
      }
    }
    .subtitle {
      font-size: 1.5rem;
      font-family: 'ZenKakuBold';
      text-align: right;
    }
  }
  .pointers {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    filter: url('#filter');
    .pointer {
      position: absolute;
      top: 0;
      left: 0;
      pointer-events: none;
      will-change: transform;
      border-radius: 50px;
      backface-visibility: hidden;
      background-color: #4062bb;
      transition: transform cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
  }
}
</style>
