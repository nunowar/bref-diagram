<script setup>
import { HugeiconsIcon } from '@hugeicons/vue';
import { DatabaseIcon } from '@hugeicons-pro/core-stroke-rounded';

defineProps({
  type: {
    type: String,
    required: true,
  },
  storage: {
    type: String,
    required: true,
  },
  usagePercent: {
    type: Number,
    required: true,
  },
  flow: {
    type: String,
    default: null,
    validator: (value) => [null, 'input', 'output', 'both'].includes(value),
  },
});
</script>

<template>
  <div class="relative w-50 rounded-xl bg-white ring-1 ring-gray-200">
    <header class="flex items-center justify-between border-b border-gray-200 p-2.5 text-gray-900">
      <div class="flex items-center space-x-1.5">
        <HugeiconsIcon :icon="DatabaseIcon" class="size-4.5 text-gray-800" />
        <span class="text-[13px] font-medium">Database</span>
      </div>
      <span class="text-xs text-gray-400">{{ type }}</span>
    </header>
    <div class="flex items-center justify-between px-2.5 py-2 text-xs text-gray-400">
      <div>
        Storage: <span class="text-gray-900">{{ storage }}</span>
      </div>
      <div class="flex items-center space-x-1">
        <span>{{ usagePercent }}%</span>
        <div class="relative h-1.5 w-12 rounded-full bg-gray-100">
          <span class="absolute top-0 h-1.5 rounded-full bg-[#3AA9E9]" :style="`width: ${usagePercent}%`"></span>
        </div>
      </div>
    </div>

    <!-- Flow indicators -->
    <span v-if="flow === 'input' || flow === 'both'" class="absolute -top-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
    <span v-if="flow === 'output' || flow === 'both'" class="absolute -bottom-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
  </div>
</template>
