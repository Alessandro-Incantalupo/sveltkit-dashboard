<script lang="ts">
  import Calendar from '$lib/components/common/Calendar.svelte';
  import Select from '$lib/components/common/Select.svelte';
  import TableUsers from '$lib/components/tables/TableUsers.svelte';
  import { Button } from '$lib/components/ui/button';

  interface Props {
    selectedProvider?: string;
    dataUsers: any[];
    headsUsers: string[];
    onDownload?: () => void;
  }

  let {
    selectedProvider = $bindable(''),
    dataUsers,
    headsUsers,
    onDownload = () => {}
  }: Props = $props();

  function handleDownload() {
    onDownload();
  }
</script>

<div class="flex flex-col gap-8">
  <!-- Mobile: Stack everything vertically -->
  <div class="block lg:hidden">
    <div class="flex flex-col gap-4">
      <!-- Select Component -->
      <Select bind:value={selectedProvider} class="w-full" />

      <!-- Calendar Components -->
      <Calendar placeholder="From" />
      <Calendar placeholder="To" />

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
