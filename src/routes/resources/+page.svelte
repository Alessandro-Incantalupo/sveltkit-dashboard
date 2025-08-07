<script lang="ts">
  import resources from '$lib/data/resources.json';

  import CardSection from '$lib/components/card-section/CardSection.svelte';
  import Table from '$lib/components/Table.svelte';
  import Tabs from '$lib/components/Tabs.svelte';
  import { Button } from '$lib/components/ui/button';
  import { Input } from '$lib/components/ui/input';
  import { toast } from 'svelte-sonner';

  let data = $state(resources);

  let activeTab = $state('All');
  let searchValue = $state('');

  const tabs = [
    { name: 'Stats', icon: 'ion:stats-chart-outline', active: false },
    { name: 'All', active: true },
    { name: 'Videos', active: false },
    { name: 'Documents', active: false },
    { name: 'Lessons', active: false },
    { name: 'Archive', active: false, disabled: true }
  ];
  const heads = ['Content Title', 'Path', 'View Count', 'Uploaded By', 'Provider', 'Type'];

  function handleTabClick(tabName: string) {
    activeTab = tabName;
  }

  function handleUpload() {
    toast.success('Resource Uploaded Successfully!', {
      duration: 3000,
      position: 'top-center'
    });
  }
</script>

<!-- Header Controls -->
<div class="mb-10 flex items-center justify-between">
  <div class="flex flex-grow items-center gap-6 border-b border-gray-300">
    <!-- Tabs -->
    <Tabs {tabs} {activeTab} onTabClick={handleTabClick} />
  </div>

  <div class="flex items-center gap-3">
    <!-- Search Input -->
    <div class="relative ml-4 w-full max-w-xs">
      <Input type="text" placeholder="Field" icon="iconamoon:search" bind:value={searchValue} />
    </div>

    <!-- Upload Button -->
    <Button onclick={handleUpload} class="bg-orange-500 hover:bg-orange-600">Upload</Button>
  </div>
</div>

{#if activeTab === 'All'}
  <Table {data} {heads} />
{:else if activeTab === 'Stats'}
  <CardSection />
{/if}
