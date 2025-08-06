<script lang="ts">
  import { page } from '$app/state';
  import Icon from '@iconify/svelte';

  const navItems = [
    { label: 'Dashboard', href: '/dashboard' },
    { label: 'Users', href: '/users' },
    { label: 'Feedbacks', href: '/feedbacks' },
    { label: 'Programs', href: '/programs' },
    { label: 'Resources', href: '/resources' },
    { label: 'Counterparties', href: '/counterparties' },
    { label: 'Events', href: '/events' }
  ];

  const navItemsWithActive = $derived(
    navItems.map(item => ({
      ...item,
      active: item.href === page.url.pathname
    }))
  );
</script>

<nav class="border-b border-sidebar-border bg-sidebar text-sidebar-foreground">
  <div class="flex items-center justify-around px-4">
    <!-- Logo Section -->
    <div class="flex items-center">
      <div class="pack-nav-brand">
        <img
          src="https://cdn.prod.website-files.com/67c5a68d264bc80704ead812/67c5aad643501555a060099a_Pack_logo%20b.png"
          alt="Pack Logo"
          class="h-8"
        />
      </div>
    </div>

    <!-- Links Section -->
    <div class="space-x-4 md:flex">
      {#each navItemsWithActive as item}
        <div class="flex h-full items-center">
          <a
            href={item.href}
            class="border-b-4 px-4 py-4 hover:text-sidebar-primary"
            class:active={item.active}
            class:border-orange-500={item.active}
            class:border-transparent={!item.active}
          >
            {item.label}
          </a>
        </div>
      {/each}
    </div>

    <!-- User Section -->
    <div class="flex items-center space-x-4">
      <!-- Country Flag -->
      <div class="h-5 w-11">
        <Icon icon="flagpack:us" class="h-full w-full rounded-lg" style="color: #3b82f6;" />
      </div>

      <!-- User Avatar -->
      <div
        class="flex h-8 w-8 items-center justify-center overflow-hidden rounded-full bg-gray-200"
      >
        <img
          src="https://via.placeholder.com/32"
          alt="User Avatar"
          class="h-full w-full object-cover"
        />
      </div>
    </div>
  </div>
</nav>
