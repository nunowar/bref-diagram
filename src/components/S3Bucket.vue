<script setup>
import { HugeiconsIcon } from '@hugeicons/vue';
import { FolderCloudIcon } from '@hugeicons-pro/core-stroke-rounded';

defineProps({
  name: {
    type: String,
    required: true,
  },
  bucketName: {
    type: String,
    default: 'Bucket name',
  },
  usedSpace: {
    type: String,
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
    <header class="flex items-center space-x-1.5 border-b border-gray-200 p-2.5 text-gray-900">
      <HugeiconsIcon :icon="FolderCloudIcon" class="size-4.5 text-gray-800" />
      <span class="text-[13px] font-medium">{{ name }}</span>
    </header>
    <div class="flex items-center justify-between px-2.5 py-2 text-xs text-gray-400">
      <div>{{ bucketName }}</div>
      <div>
        Used: <span class="text-gray-900">{{ usedSpace }}</span>
      </div>
    </div>

    <!-- Flow indicators -->
    <span v-if="flow === 'input' || flow === 'both'" class="absolute -top-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
    <span v-if="flow === 'output' || flow === 'both'" class="absolute -bottom-1 left-1/2 size-2 -translate-x-1/2 rounded-full bg-[#3AA9E9] ring-2 ring-white"></span>
  </div>
</template>
