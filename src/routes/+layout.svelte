<script lang="ts">
  import Navigation from '$lib/components/Navigation.svelte';
  import Icon from '@iconify/svelte';
  import { Toaster } from 'svelte-sonner';
  import '../app.css';

  let showChat = false;

  function toggleChat() {
    showChat = !showChat;
  }
</script>

<div class="bg-pack-neutral-50 min-h-screen">
  <Navigation />

  <main class="mx-auto max-w-7xl px-4 py-8 sm:px-6 lg:px-8">
    <slot />
  </main>

  <!-- Chat Button -->
  <button
    class="fixed right-6 bottom-6 z-50 flex h-14 w-14 items-center justify-center rounded-full bg-orange-500 text-white shadow-lg transition-colors duration-200 hover:bg-orange-600"
    on:click={toggleChat}
    aria-label="Open chat"
  >
    <Icon icon="tdesign:chat-double" class="h-6 w-6" />
    <!-- Green Circle Badge -->
    <span class="absolute bottom-1 left-10 h-4 w-4 rounded-full border-2 border-white bg-green-500"
    ></span>
  </button>
  <Toaster richColors />
</div>

<style>
</style>
