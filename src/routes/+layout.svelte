<script lang="ts">
  import Navigation from '$lib/components/Navigation.svelte';
  import { Toaster } from 'svelte-sonner';
  import '../app.css';
</script>

<div class="bg-pack-neutral-50 min-h-screen">
  <Navigation />

  <main class="container py-8">
    <slot />
  </main>
  <Toaster richColors />
</div>

<style>
</style>
