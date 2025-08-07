<script lang="ts">
  import resources from '$lib/data/resources.json';
  import userContentAccess from '$lib/data/user-content-access.json';

  import Calendar from '$lib/components/Calendar.svelte';
  import CardSection from '$lib/components/card-section/CardSection.svelte';
  import Select from '$lib/components/Select.svelte';
  import Table from '$lib/components/Table.svelte';
  import TableUsers from '$lib/components/TableUsers.svelte';
  import Tabs from '$lib/components/Tabs.svelte';
  import { Button } from '$lib/components/ui/button';
  import { Input } from '$lib/components/ui/input';
  import { toast } from 'svelte-sonner';

  let data = $state(resources);
  let dataUsers = $state(userContentAccess);

  let activeTab = $state('All');
  let searchValue = $state('');
  let selectedProvider = $state('');

  const tabs = [
    { name: 'Stats', icon: 'ion:stats-chart-outline', active: false },
    { name: 'All', active: true },
    { name: 'Videos', active: false },
    { name: 'Documents', active: false },
    { name: 'Lessons', active: false },
    { name: 'Archive', active: false, disabled: true }
  ];
  const heads = ['Content Title', 'Path', 'View Count', 'Uploaded By', 'Provider', 'Type'];
  const headsUsers = ['User', 'Accessed Content', 'Opened on', 'Closed on', 'Provider'];

  function handleTabClick(tabName: string) {
    activeTab = tabName;
  }

  function handleUpload() {
    toast.success('Resource Uploaded Successfully!', {
      duration: 3000,
      position: 'top-center'
    });
  }

  function handleDownload() {
    toast.success('Download started!', {
      duration: 3000,
      position: 'top-center'
    });
  }
</script>

<!-- Header Controls -->
<div class="mb-10 flex flex-wrap items-center justify-between gap-4">
  <div class="flex min-w-0 flex-grow items-center gap-6 border-b border-gray-300">
    <!-- Tabs -->
    <Tabs {tabs} {activeTab} onTabClick={handleTabClick} />
  </div>

  <div class="flex w-full min-w-[220px] flex-col items-center gap-3 sm:w-auto sm:flex-row">
    <div class="relative w-full max-w-xs">
      <Input type="text" placeholder="Field" icon="iconamoon:search" bind:value={searchValue} />
    </div>
    <Button onclick={handleUpload} class="w-full bg-orange-500 hover:bg-orange-600 sm:w-auto"
      >Upload</Button
    >
  </div>
</div>

{#if activeTab === 'All'}
  <Table {data} {heads} />
{:else if activeTab === 'Stats'}
  <CardSection />

  <div class="mt-8 border-t border-gray-200 pt-8">
    <h2 class="mb-4 text-2xl font-semibold">User Content Access</h2>
  </div>
  <div class="flex flex-col gap-8">
    <div class="flex items-center gap-3">
      <!-- Select Component -->
      <Select bind:value={selectedProvider} class="w-[180px] basis-1/3" />

      <!-- Calendar Components -->
      <Calendar />
      <Calendar />

      <!-- Download Button -->
      <Button onclick={handleDownload} class="bg-orange-500 hover:bg-orange-600">Download</Button>
    </div>
    <TableUsers data={dataUsers} heads={headsUsers} />
  </div>
{/if}
