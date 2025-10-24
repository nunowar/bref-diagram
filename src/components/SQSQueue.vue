<script setup>
import { HugeiconsIcon } from '@hugeicons/vue';
import { Queue01Icon } from '@hugeicons-pro/core-stroke-rounded';

defineProps({
  name: {
    type: String,
    required: true,
  },
  messages: {
    type: Number,
    required: true,
  },
  sentPerSecond: {
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
  gridCol: {
    type: Number,
    default: null,
  },
});
</script>

<template>
  <div class="relative w-50 rounded-xl bg-white ring-1 ring-gray-200">
    <header class="flex items-center space-x-1.5 border-b border-gray-200 p-2.5 text-gray-900">
      <HugeiconsIcon :icon="Queue01Icon" class="size-4.5 text-gray-800" />
      <span class="text-[13px] font-medium">{{ name }}</span>
    </header>
    <div class="flex items-center justify-between px-2.5 py-2 text-xs text-gray-400">
      <div>
        Messages: <span class="text-gray-900">{{ messages }}</span>
      </div>
      <div>
        Sent/sec: <span class="text-gray-900">{{ sentPerSecond }}</span>
      </div>
    </div>

    <!-- Flow indicators -->
    <span v-if="flow === 'input' || flow === 'both'" class="absolute -top-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
    <span v-if="flow === 'output' || flow === 'both'" class="absolute -bottom-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>

    <!-- Connectors -->
    <div v-for="(target, index) in connectTo" :key="index">
      <!-- Column 3 (gridCol=3) connectors -->
      <div v-if="gridCol === 3 && target === 'level-3-col-3'">
        <div class="pointer-events-none absolute bottom-0 left-1/2 z-50 ml-[0.5px] h-12 w-px -translate-x-full translate-y-full border-l border-[#3AA9E9]"></div>
      </div>

      <div v-if="gridCol === 3 && target === 'level-3-col-4'">
        <div class="pointer-events-none absolute bottom-0 left-[99.5px] z-50 h-6 w-40 translate-y-full border-b border-l border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute -bottom-[23px] left-[124.5px] z-50 mt-px h-6 w-50 translate-y-full border-t border-r border-[#3AA9E9]"></div>
      </div>

      <!-- Column 4 (gridCol=4) connectors -->
      <div v-if="gridCol === 4 && target === 'level-3-col-3'">
        <div class="pointer-events-none absolute right-[99.5px] bottom-0 z-50 h-6 w-40 translate-y-full border-r border-b border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute right-[124.5px] -bottom-[23px] z-50 mt-px h-6 w-50 translate-y-full border-t border-l border-[#3AA9E9]"></div>
      </div>

      <div v-if="gridCol === 4 && target === 'level-3-col-4'">
        <div class="pointer-events-none absolute bottom-0 left-1/2 z-50 ml-[0.5px] h-12 w-px -translate-x-full translate-y-full border-l border-[#3AA9E9]"></div>
      </div>

      <!-- Column 5 (gridCol=5) connectors -->
      <div v-if="gridCol === 5 && target === 'level-3-col-3'">
        <div class="pointer-events-none absolute right-[99.5px] bottom-0 z-50 h-6 w-40 translate-y-full rounded-br-lg border-r border-b border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute right-[124.5px] -bottom-[23px] z-50 mt-px h-6 w-106 translate-y-full border-t border-l border-[#3AA9E9]"></div>
      </div>

      <div v-if="gridCol === 5 && target === 'level-3-col-4'">
        <div class="pointer-events-none absolute right-[99.5px] bottom-0 z-50 h-6 w-40 translate-y-full rounded-br-lg border-r border-b border-[#3AA9E9]"></div>
        <div class="pointer-events-none absolute right-[124.5px] -bottom-[23px] z-50 mt-px h-6 w-50 translate-y-full border-t border-l border-[#3AA9E9]"></div>
      </div>
    </div>
  </div>
</template>
