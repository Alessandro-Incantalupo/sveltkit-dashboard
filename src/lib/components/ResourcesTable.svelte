<script lang="ts">
  import resources from '$lib/data/resources.json';
  import Icon from '@iconify/svelte';
  import { toast } from 'svelte-sonner';
  import { Button } from './ui/button';
  import { Input } from './ui/input';
  import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from './ui/table';

  export let data = resources;

  let activeTab = 'All';
  let searchValue = '';

  const tabs = [
    { name: 'Stats', icon: 'ion:stats-chart-outline', active: false },
    { name: 'All', active: true },
    { name: 'Videos', active: false },
    { name: 'Documents', active: false },
    { name: 'Lessons', active: false },
    { name: 'Archive', active: false, disabled: true }
  ];

  function handleTabClick(tabName: string) {
    activeTab = tabName;
  }

  function handleUpload() {
    toast.success('Resource Uploaded Successfully!', {
      duration: 3000,
      position: 'top-center'
    });
  }

  function handleSearch(event: Event) {
    const target = event.target as HTMLInputElement;
    searchValue = target.value;
  }

  // Filter data based on search
  $: filteredData = data.filter(item => {
    const matchesSearch =
      item.contentTitle.toLowerCase().includes(searchValue.toLowerCase()) ||
      item.path.toLowerCase().includes(searchValue.toLowerCase()) ||
      item.uploadedBy.toLowerCase().includes(searchValue.toLowerCase());
    return matchesSearch;
  });
</script>

<!-- Header Controls -->
<div class="mb-6 flex items-center justify-between">
  <!-- Left side: Stats icon and tabs -->
  <div class="flex flex-grow items-center gap-6 border-b border-gray-300">
    <!-- Tabs -->
    <nav class="flex space-x-8">
      {#each tabs as tab}
        <button
          class="flex items-center justify-center border-b-2 pb-2 text-sm font-medium transition-colors {activeTab ===
          tab.name
            ? 'border-blue-900 text-blue-600'
            : tab.disabled
              ? 'cursor-not-allowed border-transparent text-gray-400'
              : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700'}"
          onclick={() => !tab.disabled && handleTabClick(tab.name)}
          disabled={tab.disabled}
        >
          {#if tab.icon}
            <Icon icon={tab.icon} class="h-5 w-5" />
          {:else}
            {tab.name}
          {/if}
        </button>
      {/each}
    </nav>
  </div>

  <!-- Right side: Search and Upload -->
  <div class="flex items-center gap-3">
    <!-- Search Input -->
    <div class="relative ml-4 w-full max-w-xs">
      <Input type="text" placeholder="Field" icon="iconamoon:search" bind:value={searchValue} />
    </div>

    <!-- Upload Button -->
    <Button onclick={handleUpload} class="bg-orange-500 hover:bg-orange-600">Upload</Button>
  </div>
</div>

<!-- Table -->
<Table class="overflow-hidden rounded-lg border shadow-sm">
  <TableHeader>
    <TableRow>
      <TableHead>Content Title</TableHead>
      <TableHead>Path</TableHead>
      <TableHead>View Count</TableHead>
      <TableHead>Uploaded By</TableHead>
      <TableHead>Provider</TableHead>
      <TableHead>Type</TableHead>
      <TableHead></TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    {#each filteredData as item}
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
          <button class="text-blue-500 hover:text-blue-700 hover:underline"> View </button>
        </TableCell>
      </TableRow>
    {/each}
  </TableBody>
</Table>
