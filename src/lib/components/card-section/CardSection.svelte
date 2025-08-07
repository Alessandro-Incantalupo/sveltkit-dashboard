<script lang="ts">
  import ActiveUsersCard from './components/ActiveUsersCard.svelte';
  import LineChartCard from './components/LineChartCard.svelte';
  import MostUsedResourcesCard from './components/MostUsedResourcesCard.svelte';
  import ResourcesByCategoryCard from './components/ResourcesByCategoryCard.svelte';
  import ResourcesUtilizedCard from './components/ResourcesUtilizedCard.svelte';
  import StatsCard from './components/StatsCard.svelte';

  let activeUsersData = $state({ percentage: 37 });
  let resourcesData = $state({ percentage: 67 });
  let uploadedResources = $state({ count: 1150, change: 4 });
  let completionRate = $state({ percentage: 45, change: -10 });
  let uniqueAccesses = $state({ count: 395, total: 582, change: 3 });
</script>

<div class="flex flex-col gap-y-4 lg:gap-y-8">
  <div class="flex w-full flex-col gap-4 lg:flex-row lg:gap-x-8">
    <div class="flex flex-1 flex-col gap-y-4 lg:gap-y-8">
      <div class="flex flex-col gap-4 sm:flex-row sm:justify-between lg:gap-x-8">
        <ActiveUsersCard percentage={activeUsersData.percentage} />
        <ResourcesUtilizedCard percentage={resourcesData.percentage} />
      </div>
      <ResourcesByCategoryCard />
    </div>
    <div class="flex flex-1 flex-col justify-between gap-y-4 lg:gap-y-8">
      <StatsCard {uploadedResources} {completionRate} {uniqueAccesses} />
      <div>
        <LineChartCard />
      </div>
    </div>
  </div>

  <div class="flex flex-col gap-4 lg:flex-row lg:justify-between lg:gap-x-8">
    <MostUsedResourcesCard
      resources={[
        { title: 'How to lead new teams', url: '/resources/lead-teams', trending: null },
        { title: 'How to be more direct', url: '/resources/be-direct', trending: null },
        {
          title: 'The secret to giving great feedback',
          url: '/resources/great-feedback',
          trending: 'down'
        }
      ]}
    />
    <MostUsedResourcesCard
      resources={[
        { title: 'Conflict Resolution', url: '/resources/conflict-resolution', trending: null },
        { title: 'How to stay motivated', url: '/resources/stay-motivated', trending: 'up' },
        { title: 'Work like balance', url: '/resources/work-balance', trending: 'down' }
      ]}
    />
  </div>
</div>
