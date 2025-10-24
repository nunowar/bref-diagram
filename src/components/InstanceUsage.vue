<script setup>
import { computed } from 'vue';

const CONFIG = {
  MAX_HEIGHT: 4,
  MAX_INSTANCES: 40,
  CIRCLE_SIZE: 4,
  CIRCLE_SPACING: 2,
  OPACITY_THRESHOLDS: [
    { max: 4, opacity: 0.1 },
    { max: 8, opacity: 0.25 },
    { max: 12, opacity: 0.4 },
    { max: 16, opacity: 0.6 },
    { max: 20, opacity: 0.8 },
    { max: Infinity, opacity: 1 },
  ],
};

const props = defineProps({
  instances: {
    type: Array,
    required: true,
    validator: (value) => Array.isArray(value) && value.every((item) => typeof item === 'object' && typeof item.used === 'number'),
  },
});

const getOpacity = (usedHours) => {
  const threshold = CONFIG.OPACITY_THRESHOLDS.find((t) => usedHours <= t.max);
  return threshold?.opacity ?? 1;
};

const circleColumns = computed(() => {
  if (!props.instances.length) return [];

  const sortedInstances = [...props.instances].sort((a, b) => b.used - a.used).slice(0, CONFIG.MAX_INSTANCES);

  const columns = [];

  for (let i = 0; i < sortedInstances.length; i += CONFIG.MAX_HEIGHT) {
    const columnCircles = sortedInstances
      .slice(i, i + CONFIG.MAX_HEIGHT)
      .map((instance) => ({
        opacity: getOpacity(instance.used),
        used: instance.used,
      }))
      .reverse(); // Reverse so they stack bottom to top

    columns.push(columnCircles);
  }

  return columns;
});
</script>

<template>
  <div class="flex flex-row-reverse items-end justify-end" :aria-label="`${instances.length} instances visualization`" role="img" :style="{ gap: `${CONFIG.CIRCLE_SPACING}px` }">
    <div v-for="(column, colIndex) in circleColumns" :key="`col-${colIndex}`" class="flex flex-col justify-end" :style="{ gap: `${CONFIG.CIRCLE_SPACING}px` }">
      <span
        v-for="(circle, circleIndex) in column"
        :key="`circle-${colIndex}-${circleIndex}`"
        class="flex-shrink-0 rounded-full bg-[#3AA9E9]"
        :style="{
          width: `${CONFIG.CIRCLE_SIZE}px`,
          height: `${CONFIG.CIRCLE_SIZE}px`,
          opacity: circle.opacity,
        }"
        :title="`${circle.used} hours used`"
      />
    </div>
  </div>
</template>
