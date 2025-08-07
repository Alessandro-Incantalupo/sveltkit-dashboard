<script lang="ts">
  import Icon from '@iconify/svelte';
  import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from './ui/table';

  const { data = [], heads = [] } = $props<{ data?: any[]; heads?: string[] }>();
</script>

<Table class="overflow-hidden rounded-lg border shadow-sm">
  <TableHeader>
    <TableRow>
      {#each heads as head, i}
        <TableHead>
          {head}
          {#if i === 0}
            <Icon icon="mdi:arrow-down" class="ml-2 inline-block h-4 w-4" />
          {/if}
        </TableHead>
      {/each}
      <TableHead></TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    {#each data as item}
      <TableRow class="hover:bg-gray-50">
        {#each Object.entries(item) as [key, value]}
          <TableCell class="text-gray-600">
            {#if typeof value === 'string' || typeof value === 'number'}
              {value}
            {:else}
              <!-- Handle non-primitive values if needed -->
              <span class="text-gray-400">N/A</span>
            {/if}
          </TableCell>
        {/each}
        <TableCell>
          <button> ... </button>
        </TableCell>
      </TableRow>
    {/each}
  </TableBody>
</Table>
