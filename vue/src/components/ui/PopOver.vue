<template>
  <span class="popover__container" @mouseover="show = true" @mouseleave="show = false">
    <slot />
    <transition name="popover__fade">
      <div v-if="show" class="popover">
        <slot name="popover"/>
      </div>
    </transition>
  </span>
</template>

<script>
export default {
  data () {
    return {
      show: false
    }
  }
}
</script>

<style lang="less" scoped>
.popover {
  position: absolute;
  top: calc(100% + 5px);
  left: calc(50%);
  transform: translateX(-50%);
  transition: 0.3s ease;

  &__container {
    position: relative;
    display: inline-block;
  }

  &__fade-enter-active, &__fade-leave-active {
    transition: 0.3s ease;
  }

  &__fade-enter, &__fade-leave-to {
    opacity: 0;
  }
}
</style>
