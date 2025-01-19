<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';
const { size, timeElapsed } = defineProps<{ size: number; timeElapsed: number }>();
const timeSpawned = ref(timeElapsed);
const previousTimestamp = ref(timeElapsed);
const isFalling = ref(true);
const ACCELERATION = 49; // pixels per second squared

const calculatedSize = computed(() => {
    // 5 is a multiplier since i am representing 100m into 500px
    return size * 5;
});

onMounted(() => {
    const circle = document.getElementById("circle")!;
    const spaceRect = document.getElementById("space")!.getBoundingClientRect();
    circle.style.top = "0"

    function fall(t: number) {
        const circleRect = circle.getBoundingClientRect();

        // Stop falling if the circle reaches the bottom of the space
        if (circleRect.bottom >= spaceRect.bottom) {
            isFalling.value = false;
            return;
        }

        // Time elapsed since the circle was spawned, in seconds
        const timeSinceSpawn = (t - timeSpawned.value) / 1_000;

        // Distance traveled under constant acceleration
        const distance = (0.5 * ACCELERATION * timeSinceSpawn ** 2);

        // Set the new position of the circle
        circle.style.top = `${distance}px`;

        // Store the current timestamp for the next frame
        previousTimestamp.value = t;
        // Request the next frame
        requestAnimationFrame(fall);
    }

        timeSpawned.value = performance.now(); // Reset spawn time to the current time
        requestAnimationFrame(fall);
});
</script>

<template>
    <div id="circle" class="absolute shadow-sm bg-green-200 rounded-full" :style="{width: `${calculatedSize}px`, height: `${calculatedSize}px`}">
    </div>
</template>
