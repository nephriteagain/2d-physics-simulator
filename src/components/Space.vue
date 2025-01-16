<script setup lang="ts">
defineProps<{timeElapsed: number}>()

</script>

<template>
  <div id="space" class="relative w-[1000px] h-[500px] bg-blue-200">
      <p class="absolute top-1 right-1">100m</p>
      <p>{{ Math.round(timeElapsed / 1000) }} has passed</p>
      <slot></slot>
    </div>
</template>

<style scoped>
</style>
