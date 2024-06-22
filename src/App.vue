<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="container">
    <Transition name="switch-page" mode="out-in">
      <RouterView/>
    </Transition>
  </div>
</template>

<style scoped>
.container {
  max-width: 1000px;
  margin: 0 auto;
}

.switch-page-enter-active,
.switch-page-leave-active {
  transition: all 0.5s ease;
}

.switch-page-enter-from,
.switch-page-leave-to {
  opacity: 0;
  transform: translateX(50px)
}
</style>