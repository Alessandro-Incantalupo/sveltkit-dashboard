<script lang="ts">
  export type Resource = {
    title: string;
    url: string;
    trending: 'up' | 'down' | null;
  };
  import * as Card from '$lib/components/ui/card/index.js';
  import Icon from '@iconify/svelte';
  import { toast } from 'svelte-sonner';

  const { resources = [] } = $props<{ resources?: Resource[] }>();

  function handleResourceClick(event: MouseEvent, resourceTitle: string) {
    event.preventDefault();
    toast.info(`"Work in progress"`, {
      description: 'This feature will be available soon!',
      duration: 3000
    });
  }
</script>

<Card.Root class="flex w-full gap-1 p-4">
  <div class=" text-sm font-semibold text-gray-500">Most Used resources</div>
  <ul class="space-y-2">
    {#each resources as resource}
      <li class="flex items-center justify-between">
        <a
          href="javascript:void(0)"
          class=" flex items-center gap-2 text-lg font-medium underline hover:underline"
          onclick={event => handleResourceClick(event, resource.title)}
        >
          {resource.title}
        </a>
        {#if resource.trending === 'up'}
          <Icon icon="ic:round-trending-up" class="h-4 w-4 text-green-600" />
        {:else if resource.trending === 'down'}
          <Icon icon="ic:round-trending-down" class="h-4 w-4 text-red-600" />
        {/if}
      </li>
    {/each}
  </ul>
</Card.Root>
