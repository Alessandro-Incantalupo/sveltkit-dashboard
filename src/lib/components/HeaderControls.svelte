<script lang="ts">
  import Tabs from '$lib/components/Tabs.svelte';
  import { Button } from '$lib/components/ui/button';
  import { Input } from '$lib/components/ui/input';

  interface Tab {
    name: string;
    icon?: string;
    active: boolean;
    disabled?: boolean;
  }

  interface Props {
    tabs: Tab[];
    activeTab: string;
    searchValue?: string;
    onTabClick?: (tabName: string) => void;
    onUpload?: () => void;
  }

  let {
    tabs,
    activeTab,
    searchValue = $bindable(''),
    onTabClick = () => {},
    onUpload = () => {}
  }: Props = $props();

  function handleTabClick(tabName: string) {
    onTabClick(tabName);
  }

  function handleUpload() {
    onUpload();
  }
</script>

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
