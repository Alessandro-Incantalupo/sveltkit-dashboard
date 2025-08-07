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
        <TableCell class="font-medium">{item.contentTitle}</TableCell>
        <TableCell class="text-gray-600">{item.path}</TableCell>
        <TableCell>{item.viewCount}</TableCell>
        <TableCell>{item.uploadedBy}</TableCell>
        <TableCell>
          <span class="rounded-full bg-gray-100 px-2 py-1 text-xs font-medium text-gray-700">
            {item.provider}
          </span>
        </TableCell>
        <TableCell>
          <span class="rounded-full bg-gray-100 px-2 py-1 text-xs font-medium text-gray-700">
            {item.type}
          </span>
        </TableCell>
        <TableCell>
          <button class="hover:text-blue-700 hover:underline"> ... </button>
        </TableCell>
      </TableRow>
    {/each}
  </TableBody>
</Table>
