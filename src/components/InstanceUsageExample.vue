<script setup>
import InstanceUsage from './InstanceUsage.vue';
</script>

<template>
  <div class="space-y-4">
    <h2 class="text-lg font-semibold">Instance Usage (Last 24h)</h2>
    <div class="flex flex-wrap gap-10 space-y-4">
      <div class="space-y-8">
        <div>
          <div class="mb-2 text-sm text-gray-600">11 instances</div>
          <InstanceUsage :instances="[{ used: 24 }, { used: 20 }, { used: 16 }, { used: 12 }, { used: 24 }, { used: 20 }, { used: 16 }, { used: 12 }, { used: 8 }, { used: 4 }, { used: 1 }]" />
        </div>

        <div>
          <div class="mb-2 text-sm text-gray-600">40 instances</div>
          <InstanceUsage :instances="[{ used: 24 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }, { used: 24 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }, { used: 24 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }, { used: 24 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }, { used: 24 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }, { used: 22 }, { used: 21 }, { used: 8 }, { used: 2 }, { used: 5 }, { used: 8 }]" />
        </div>
      </div>

      <div>
        <h3 class="mb-2 text-sm font-medium">Legend:</h3>
        <ul class="space-y-1 text-xs text-gray-600">
          <li><span class="text-[#3AA9E9] opacity-100">●</span> 20-24 hours (full opacity)</li>
          <li><span class="text-[#3AA9E9] opacity-80">●</span> 16-20 hours (80% opacity)</li>
          <li><span class="text-[#3AA9E9] opacity-60">●</span> 12-16 hours (60% opacity)</li>
          <li><span class="text-[#3AA9E9] opacity-40">●</span> 8-12 hours (40% opacity)</li>
          <li><span class="text-[#3AA9E9] opacity-20">●</span> 4-8 hours (20% opacity)</li>
          <li><span class="text-[#3AA9E9] opacity-10">●</span> 1-4 hours (10% opacity)</li>
        </ul>
      </div>
    </div>
  </div>
</template>
