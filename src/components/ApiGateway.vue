<script setup>
import { HugeiconsIcon } from '@hugeicons/vue';
import { CpuIcon } from '@hugeicons-pro/core-stroke-rounded';

defineProps({
  referenceId: {
    type: String,
    default: 'Reference ID',
  },
  info: {
    type: String,
    default: 'More info',
  },
  flow: {
    type: String,
    default: null,
    validator: (value) => [null, 'input', 'output', 'both'].includes(value),
  },
  connectTo: {
    type: Array,
    default: () => [],
  },
});
</script>

<template>
  <div class="relative w-50 rounded-xl bg-white ring-1 ring-gray-200">
    <header class="flex items-center space-x-1.5 border-b border-gray-200 p-2.5 text-gray-900">
      <HugeiconsIcon :icon="CpuIcon" class="size-4.5 text-gray-800" />
      <span class="text-[13px] font-medium">API Gateway</span>
    </header>
    <div class="flex items-center justify-between px-2.5 py-2 text-xs text-gray-400">
      <div>{{ referenceId }}</div>
      <div>{{ info }}</div>
    </div>

    <!-- Flow indicators -->
    <span v-if="flow === 'input' || flow === 'both'" class="absolute -top-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
    <span v-if="flow === 'output' || flow === 'both'" class="absolute -bottom-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>

    <!-- Connectors -->
    <div v-for="(target, index) in connectTo" :key="index">
      <div v-if="target === 'level-3-col-1'">
        <div class="pointer-events-none absolute bottom-0 left-1/2 z-50 ml-[0.5px] h-12 w-px -translate-x-full translate-y-full border-r border-[#3AA9E9]"></div>
      </div>
    </div>
  </div>
</template>
