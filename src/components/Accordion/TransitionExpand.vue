<template>
  <transition
    name="expand"
    @enter="enter"
    @after-enter="afterEnter"
    @leave="leave"
    @after-leave="afterLeave"
  >
    <slot />
  </transition>
</template>

<script>
export default {
  name: 'transition-expand',
  methods: {
    enter(el) {
      const element = el;
      const { width } = getComputedStyle(element);

      element.style.width = width;
      element.style.position = 'absolute';
      element.style.visibility = 'hidden';
      element.style.height = 'auto';

      const { height } = getComputedStyle(element);

      element.style.width = null;
      element.style.position = null;
      element.style.visibility = null;
      element.style.height = 0;

      /* eslint-disable no-unused-expressions */
      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height;
      /* eslint-disable no-unused-expressions */

      // Trigger the animation.
      // We use `requestAnimationFrame` because we need
      // to make sure the browser has finished
      // painting after setting the `height`
      // to `0` in the line above.
      requestAnimationFrame(() => {
        element.style.height = height;
      });
    },
    afterEnter(el) {
      const element = el;
      element.style.height = 'auto';
      this.$emit('expanded');
    },
    leave(el) {
      const element = el;
      const { height } = getComputedStyle(element);
      element.style.height = height;

      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height;

      requestAnimationFrame(() => {
        element.style.height = 0;
      });
    },
    afterLeave() {
      this.$emit('contracted');
    },
  },
};
</script>

<style lang="postcss">
.expand-enter-active,
.expand-leave-active {
  transition: height 0.5s ease-in-out;
  overflow: hidden;
}

.expand-enter,
.expand-leave-to {
  height: 0;
}
</style>

<style scoped>
* {
  will-change: height;
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
</style>
