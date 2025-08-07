<script lang="ts">
  import * as Chart from 'chart.js';
  import { onMount } from 'svelte';
  import ActiveUsersCard from './components/ActiveUsersCard.svelte';
  import ResourcesByCategoryCard from './components/ResourcesByCategoryCard.svelte';
  import ResourcesUtilizedCard from './components/ResourcesUtilizedCard.svelte';
  import StatsCard from './components/StatsCard.svelte';

  let activeUsersData = $state({ percentage: 37 });
  let resourcesData = $state({ percentage: 67 });
  let uploadedResources = $state({ count: 1150, change: 4 });
  let completionRate = $state({ percentage: 45, change: -10 });
  let uniqueAccesses = $state({ count: 395, total: 582, change: 3 });

  let activeUsersCanvas: HTMLCanvasElement;
  let resourcesCanvas: HTMLCanvasElement;
  let activeUsersChart: Chart.Chart;
  let resourcesChart: Chart.Chart;

  onMount(() => {
    // Register Chart.js components
    Chart.Chart.register(...Chart.registerables);

    // Active Users Doughnut Chart
    activeUsersChart = new Chart.Chart(activeUsersCanvas, {
      type: 'doughnut',
      data: {
        datasets: [
          {
            data: [activeUsersData.percentage, 100 - activeUsersData.percentage],
            backgroundColor: ['#3b82f6', '#e5e7eb'],
            borderWidth: 0,
            cutout: '75%'
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: true,
        plugins: {
          legend: {
            display: false
          },
          tooltip: {
            enabled: false
          }
        }
      }
    });

    // Resources Doughnut Chart
    resourcesChart = new Chart.Chart(resourcesCanvas, {
      type: 'doughnut',
      data: {
        datasets: [
          {
            data: [resourcesData.percentage, 100 - resourcesData.percentage],
            backgroundColor: ['#f97316', '#e5e7eb'],
            borderWidth: 0,
            cutout: '75%'
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: true,
        plugins: {
          legend: {
            display: false
          },
          tooltip: {
            enabled: false
          }
        }
      }
    });
  });
</script>

<div class="flex flex-col">
  <div class="flex w-full gap-x-8">
    <!-- Left column: cards stacked vertically -->
    <div class=" flex flex-1 flex-col gap-y-8">
      <div class="flex justify-between gap-x-8">
        <ActiveUsersCard percentage={activeUsersData.percentage} />
        <ResourcesUtilizedCard percentage={resourcesData.percentage} />
      </div>
      <ResourcesByCategoryCard />
    </div>
    <!-- Right column: stats card fills vertical space -->
    <div class="flex flex-1 flex-col gap-y-8">
      <StatsCard {uploadedResources} {completionRate} {uniqueAccesses} />
      <div></div>
    </div>
  </div>

  <div class="grid grid-cols-1 gap-4 lg:col-span-3 lg:grid-cols-2">
    <!-- <ResourcesByCategoryCard />
    <LineChartCard /> -->
  </div>
  <div class="grid grid-cols-1 gap-4 lg:col-span-3 lg:grid-cols-2">
    <!-- <MostUsedResourcesCard side="left" />
    <MostUsedResourcesCard side="right" /> -->
  </div>
</div>
