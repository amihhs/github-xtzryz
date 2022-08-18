<script setup lang='ts'>
import { isClient, useWindowScroll } from '@vueuse/core'
const isVisibleHeader = ref(false)
if (isClient) {
  const { y } = useWindowScroll()
  watch(y, (newValue, oldValue) => {
    if (newValue > oldValue && newValue > 200)
      isVisibleHeader.value = true
    else if (newValue < oldValue)
      isVisibleHeader.value = false
  })
}
</script>

<template>
  <div
    class="default-header transition"
    :class="{ 'header-hidden': isVisibleHeader }"
  >
    <div
      flex
      items-center
      justify-between
      m-auto
      px-5
      h-full
      max="w-1440px"
    >
      <nuxt-link to="/">
        <div
          class="logo text-8 font-bold"
          sm="text-10"
        >
          LOGO
        </div>
      </nuxt-link>
      <div class="setting" />
    </div>
  </div>
  <div
    class="default-header-place"
    :class="{ 'header-hidden': isVisibleHeader }"
  />
</template>

<style lang='scss' scoped>
.default-header {
  @apply fixed w-full top-0 z-999 shadow-lg backdrop-blur-md bg-white bg-opacity-60 dark:bg-dark-800 h-15 sm:h-20;
}

.default-header-place {
  @apply w-full top-0 z-1 h-15 sm:h-20;
}

.header-hidden {
  transform: translate3d(0, -100%, 0);
}
</style>
