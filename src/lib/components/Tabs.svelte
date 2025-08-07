<script lang="ts">
  import Icon from '@iconify/svelte';

  const {
    tabs = [],
    activeTab,
    onTabClick = () => {}
  } = $props<{
    tabs?: { name: string; icon?: string; active?: boolean; disabled?: boolean }[];
    activeTab?: string;
    onTabClick?: (tabName: string) => void;
  }>();
</script>

<div class="flex flex-grow items-center gap-6 border-b border-gray-300">
  <nav class="flex space-x-6 md:space-x-8">
    {#each tabs as tab}
      <button
        class="flex items-center justify-center border-b-2 pb-2 text-sm font-medium transition-colors {activeTab ===
        tab.name
          ? 'border-blue-900 text-blue-600'
          : tab.disabled
            ? 'cursor-not-allowed border-transparent text-gray-400'
            : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700'}"
        onclick={() => !tab.disabled && onTabClick(tab.name)}
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
