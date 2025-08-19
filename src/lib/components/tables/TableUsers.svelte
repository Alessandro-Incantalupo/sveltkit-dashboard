<script lang="ts">
  import * as Avatar from '$lib/components/ui/avatar/index.js';
  import Icon from '@iconify/svelte';
  import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '../ui/table';

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
        <!-- User Avatar and Name -->
        <TableCell class="flex items-center gap-3">
          <Avatar.Root>
            <Avatar.Image
              src="https://github.com/shadcn.png"
              alt="@shadcn"
              class="h-8 w-8 rounded-full"
            />
            <Avatar.Fallback class="h-8 w-8 rounded-full bg-gray-300 text-center"
              >CN</Avatar.Fallback
            >
          </Avatar.Root>
          <div>
            <div class="font-medium text-gray-800">{item.user}</div>
            <div class="text-sm text-gray-500">Role</div>
          </div>
        </TableCell>

        <!-- Accessed Content -->
        <TableCell class="text-gray-600">{item.accessedContent}</TableCell>

        <!-- Opened On -->
        <TableCell>{item.openedOn}</TableCell>

        <!-- Closed On -->
        <TableCell>{item.closedOn}</TableCell>

        <!-- Provider Badge -->
        <TableCell>
          <span
            class="rounded-full border-2 px-2 py-1 text-xs font-medium"
            class:border-orange-500={item.provider === 'Pack'}
            class:border-green-500={item.provider === 'Mentor'}
            class:text-orange-500={item.provider === 'Pack'}
            class:text-green-500={item.provider === 'Mentor'}
          >
            {item.provider}
          </span>
        </TableCell>

        <!-- Actions -->
        <TableCell>
          <button class="hover:text-blue-700 hover:underline"> ... </button>
        </TableCell>
      </TableRow>
    {/each}
  </TableBody>
</Table>
