<script setup>
import { HugeiconsIcon } from '@hugeicons/vue';
import { AiCloud02Icon } from '@hugeicons-pro/core-stroke-rounded';

defineProps({
  distributionId: {
    type: String,
    required: true,
  },
  nodes: {
    type: Number,
    required: true,
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
      <HugeiconsIcon :icon="AiCloud02Icon" class="size-4.5 text-gray-800" />
      <span class="text-[13px] font-medium">CloudFront CDN</span>
    </header>
    <div class="flex items-center justify-between px-2.5 py-2 text-xs text-gray-400">
      <div>{{ distributionId }}</div>
      <div>
        Nodes: <span class="text-gray-900">{{ nodes }}</span>
      </div>
    </div>

    <!-- Flow indicators -->
    <span v-if="flow === 'input' || flow === 'both'" class="absolute -top-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
    <span v-if="flow === 'output' || flow === 'both'" class="absolute -bottom-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>

    <!-- Connectors -->
    <div v-for="(target, index) in connectTo" :key="index">
      <div v-if="target === 'level-2-col-1'">
        <div class="pointer-events-none absolute bottom-0 left-1/2 ml-[0.5px] h-6 w-[60px] -translate-x-full translate-y-full rounded-br-lg border-r border-b border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute -bottom-[23px] left-[60px] h-6 w-[72.5px] -translate-x-full translate-y-full rounded-tl-lg border-t border-l border-[#3AA9E9]"></div>
      </div>

      <div v-if="target === 'level-2-col-2'">
        <div class="pointer-events-none absolute right-1/2 bottom-0 mr-[0.5px] h-6 w-[60px] translate-x-full translate-y-full rounded-bl-lg border-b border-l border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute right-[60px] -bottom-[23px] h-6 w-[72.5px] translate-x-full translate-y-full rounded-tr-lg border-t border-r border-[#3AA9E9]"></div>
      </div>
    </div>
  </div>
</template>
