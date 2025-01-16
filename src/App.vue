<script setup lang="ts">
import Space from './components/Space.vue';
import Circle from './components/Circle.vue';
import { ref, onMounted } from 'vue';
document.title = "2d physics engine"
const timeElapsed = ref(0)

onMounted(() => {
    function gravity(t:number) {
        timeElapsed.value = t
        requestAnimationFrame(gravity)
    }

    requestAnimationFrame(gravity)
})


</script>

<template>
  <div class="w-screen h-screen flex flex-col items-center justify-center">
    <Space :timeElapsed="timeElapsed">
      <Circle :size="5" :timeElapsed="timeElapsed" />
    </Space>
    
  </div>
</template>

<style scoped>

</style>
