<script lang="ts">
  import resources from '$lib/data/resources.json';
  import userContentAccess from '$lib/data/user-content-access.json';

  import Calendar from '$lib/components/Calendar.svelte';
  import CardSection from '$lib/components/card-section/CardSection.svelte';
  import Select from '$lib/components/Select.svelte';
  import SelectForm from '$lib/components/SelectForm.svelte';
  import Table from '$lib/components/Table.svelte';
  import TableUsers from '$lib/components/TableUsers.svelte';
  import Tabs from '$lib/components/Tabs.svelte';
  import { Button } from '$lib/components/ui/button';
  import * as Dialog from '$lib/components/ui/dialog/index.js';
  import { Input } from '$lib/components/ui/input';
  import { toast } from 'svelte-sonner';

  let data = $state(resources);
  let dataUsers = $state(userContentAccess);

  let activeTab = $state('All');
  let searchValue = $state('');
  let selectedProvider = $state('');

  let uploadDialogOpen = $state(false);
  let uploadTitle = $state('');
  let uploadFile = $state(null);
  let uploadProvider = $state('');
  let uploadType = $state('');
  let uploadDescription = $state('');
  let uploadCategory = $state('');
  let uploadLanguage = $state('');
  let uploadRole = $state('');

  // Options for different selects
  const categoryOptions = [
    { label: 'Video', value: 'video' },
    { label: 'Document', value: 'document' },
    { label: 'Lesson', value: 'lesson' },
    { label: 'Tutorial', value: 'tutorial' }
  ];

  const languageOptions = [
    { label: 'English', value: 'english' },
    { label: 'Spanish', value: 'spanish' },
    { label: 'French', value: 'french' },
    { label: 'German', value: 'german' }
  ];

  const providerOptions = [
    { label: 'Pack', value: 'pack' },
    { label: 'Mentor', value: 'mentor' },
    { label: 'External', value: 'external' },
    { label: 'Internal', value: 'internal' },
    { label: 'Partner', value: 'partner' }
  ];

  const roleOptions = [
    { label: 'Mentor / Coach', value: 'mentor' },
    { label: 'Mentee / Coachee', value: 'mentee' }
  ];

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
  function handleDownload() {
    toast.success('Download started!', {
      duration: 3000,
      position: 'top-center'
    });
  }

  function handleUpload() {
    uploadDialogOpen = true;
  }

  function handleSubmitUpload() {
    toast.success('Resource Uploaded Successfully!', {
      duration: 3000,
      position: 'top-center'
    });

    uploadTitle = '';
    uploadFile = null;
    uploadProvider = '';
    uploadType = '';
    uploadDialogOpen = false;
    uploadDescription = '';
    uploadCategory = '';
    uploadLanguage = '';
    uploadRole = '';
  }
</script>

<!-- Upload Dialog -->
<Dialog.Root bind:open={uploadDialogOpen}>
  <Dialog.Content class="sm:max-w-[500px]">
    <Dialog.Header>
      <Dialog.Title>Upload Resource</Dialog.Title>
    </Dialog.Header>
    <div class="grid gap-4 py-4">
      <Input id="title" bind:value={uploadTitle} placeholder="Title*" />
      <Input id="description" bind:value={uploadDescription} placeholder="Description*" />

      <SelectForm
        bind:value={uploadCategory}
        options={categoryOptions}
        placeholder="Category*"
        label="Categories"
        name="category"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadLanguage}
        options={languageOptions}
        placeholder="Language*"
        label="Languages"
        name="language"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadProvider}
        options={providerOptions}
        placeholder="Provider*"
        label="Providers"
        name="provider"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadRole}
        options={roleOptions}
        placeholder="Role"
        label="Roles"
        name="role"
        class="w-full"
      />

      <div class="flex gap-3">
        <Input id="file" type="file" placeholder="No file selected*" class="flex-1" />
        <Button variant="outline" class="whitespace-nowrap">Select file</Button>
      </div>
    </div>
    <Dialog.Footer>
      <Button type="submit" onclick={handleSubmitUpload} class="bg-orange-500 hover:bg-orange-600"
        >Upload</Button
      >
    </Dialog.Footer>
  </Dialog.Content>
</Dialog.Root>

<!-- Header Controls -->
<div class="mb-10 space-y-4">
  <!-- Mobile: Stack everything vertically -->
  <div class="block lg:hidden">
    <!-- Search and Upload Button Row -->
    <div class="mb-4 flex flex-col gap-3 sm:flex-row">
      <div class="flex-1">
        <Input
          type="text"
          placeholder="Search resources..."
          icon="iconamoon:search"
          bind:value={searchValue}
          class="w-full"
        />
      </div>
      <Button onclick={handleUpload} class="bg-orange-500 whitespace-nowrap hover:bg-orange-600">
        Upload
      </Button>
    </div>

    <!-- Tabs Row - Fixed container with proper overflow handling -->
    <div class="overflow-x-auto border-b border-gray-300">
      <div class="min-w-max">
        <Tabs {tabs} {activeTab} onTabClick={handleTabClick} />
      </div>
    </div>
  </div>

  <!-- Desktop: Horizontal layout -->
  <div class="hidden lg:flex lg:items-center lg:justify-between lg:gap-6">
    <!-- Left: Tabs -->
    <div class="flex min-w-0 flex-1 overflow-x-auto border-b border-gray-300">
      <div class="min-w-max">
        <Tabs {tabs} {activeTab} onTabClick={handleTabClick} />
      </div>
    </div>

    <!-- Right: Search and Upload -->
    <div class="flex flex-shrink-0 items-center gap-3">
      <div class="w-80">
        <Input
          type="text"
          placeholder="Search resources..."
          icon="iconamoon:search"
          bind:value={searchValue}
        />
      </div>
      <Button onclick={handleUpload} class="bg-orange-500 whitespace-nowrap hover:bg-orange-600">
        Upload
      </Button>
    </div>
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
    <!-- Mobile: Stack everything vertically -->
    <div class="block lg:hidden">
      <div class="flex flex-col gap-4">
        <!-- Select Component -->
        <Select bind:value={selectedProvider} class="w-full" />

        <!-- Calendar Components -->
        <Calendar />
        <Calendar />

        <!-- Download Button -->
        <Button onclick={handleDownload} class="w-full bg-orange-500 hover:bg-orange-600">
          Download
        </Button>
      </div>
    </div>

    <!-- Desktop: Horizontal layout with basis -->
    <div class="hidden lg:flex lg:items-center lg:gap-3">
      <!-- Select Component -->
      <Select bind:value={selectedProvider} class="basis-1/3" />

      <!-- Calendar Components -->
      <Calendar placeholder="From" />
      <Calendar placeholder="To" />

      <!-- Download Button -->
      <Button onclick={handleDownload} class=" bg-orange-500 whitespace-nowrap hover:bg-orange-600">
        Download
      </Button>
    </div>

    <TableUsers data={dataUsers} heads={headsUsers} />
  </div>
{/if}
