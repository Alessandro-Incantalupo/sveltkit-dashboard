<script lang="ts">
  import { Badge } from '$lib/components/ui/badge/index.js';
  import * as Card from '$lib/components/ui/card/index.js';
  import Icon from '@iconify/svelte';
  export let uploadedResources;
  export let completionRate;
  export let uniqueAccesses;
</script>

<Card.Root class="p-6">
  <div class="flex h-full">
    <!-- Resources Uploaded -->
    <div class="flex flex-1 flex-col items-center justify-center">
      <div class="mb-2 flex items-center gap-2 text-sm font-semibold text-gray-500">
        <Icon icon="mdi:file-document-outline" width="20" height="20" />
        <span>Resources Uploaded</span>
      </div>
      <div class="flex items-center">
        <span class="mb-2 text-2xl font-bold">{uploadedResources.count}</span>
        <Badge
          variant="outline"
          class="text-md flex translate-y-1 items-center gap-0 border-none bg-transparent px-0 font-bold text-green-600 shadow-none"
        >
          <Icon icon="ic:round-trending-up" class="!h-4 !w-4 font-bold text-green-700" />
          +{uploadedResources.change}%
        </Badge>
      </div>
    </div>
    <div class="mx-4 w-px bg-gray-200"></div>
    <!-- Completion Rate -->
    <div class="flex flex-1 flex-col items-center justify-center">
      <div class="mb-2 flex items-center gap-2 text-sm font-semibold text-gray-500">
        <Icon icon="streamline:play-list-9" width="20" height="20" class="text-gray-400" />
        <span>Completion Rate</span>
      </div>
      <div class="flex items-center">
        <span class="mb-2 text-2xl font-bold">{completionRate.percentage}%</span>
        <Badge
          variant="outline"
          class="text-md flex translate-y-1 items-center gap-0 border-none bg-transparent px-0 font-bold text-red-600 shadow-none"
        >
          <Icon icon="ic:round-trending-down" class="!h-4 !w-4 font-bold text-red-700" />
          {completionRate.change}%
        </Badge>
      </div>
    </div>
    <div class="mx-4 w-px bg-gray-200"></div>
    <!-- Unique Accesses -->
    <div class="flex flex-1 flex-col items-center justify-center">
      <div class="mb-2 flex items-center gap-2 text-sm font-semibold text-gray-500">
        <Icon icon="ion:stats-chart-outline" width="20" height="20" class="text-gray-400" />
        <span>Unique Accesses</span>
      </div>
      <div class="flex items-center">
        <span class="mb-2 text-2xl font-bold">{uniqueAccesses.count}/{uniqueAccesses.total}</span>
        <Badge
          variant="outline"
          class="text-md flex translate-y-1 items-center gap-0 border-none bg-transparent px-0 font-bold text-green-600 shadow-none"
        >
          <Icon icon="ic:round-trending-up" class="!h-4 !w-4 font-bold text-green-700" />
          +{uniqueAccesses.change}%
        </Badge>
      </div>
    </div>
  </div>
</Card.Root>
