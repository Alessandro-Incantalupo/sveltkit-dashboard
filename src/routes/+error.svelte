<script lang="ts">
  import Icon from '@iconify/svelte';
</script>

<div class="flex min-h-96 items-center justify-center">
  <div class="text-center">
    <h2 class="mb-2 text-2xl font-semibold">Resource Not Found</h2>
    <p class="mb-4 text-gray-600">
      The resource you're looking for doesn't exist or has been removed.
    </p>
    <a
      href="/resources"
      class="inline-flex items-center gap-2 rounded-lg bg-orange-500 px-4 py-2 text-white hover:bg-orange-600"
    >
      <Icon icon="mdi:arrow-left" class="h-4 w-4" />
      Back to Resources
    </a>
  </div>
</div>
