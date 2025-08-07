<script lang="ts">
  import * as Card from '$lib/components/ui/card/index.js';
  import * as Chart from 'chart.js';
  import { onMount } from 'svelte';

  let categories = [
    { label: 'Category', value: 60, color: '#f97316' },
    { label: 'Category', value: 28, color: '#fdba74' },
    { label: 'Category', value: 12, color: '#fbbf24' }
  ];

  let canvas: HTMLCanvasElement;
  let chart: Chart.Chart;

  onMount(() => {
    Chart.Chart.register(...Chart.registerables);
    chart = new Chart.Chart(canvas, {
      type: 'pie',
      data: {
        labels: categories.map(c => `${c.value}% ${c.label}`),
        datasets: [
          {
            data: categories.map(c => c.value),
            backgroundColor: categories.map(c => c.color),
            borderWidth: 0
          }
        ]
      },
      options: {
        rotation: -215,
        responsive: true,
        maintainAspectRatio: true,
        plugins: {
          legend: { display: false },
          tooltip: { enabled: true }
        }
      }
    });
  });
</script>

<Card.Root class="flex flex-col items-center justify-center px-10 py-4">
  <Card.Content class="flex flex-col items-center space-y-6">
    <span class="mb-2 -translate-x-23 text-lg font-semibold">Resources by category</span>
    <div class="flex items-center gap-8">
      <div class="flex h-44 w-44 items-center justify-center">
        <canvas bind:this={canvas} class="h-44 w-44"></canvas>
      </div>
      <div class="flex flex-col items-start space-y-4">
        {#each categories as cat}
          <div class="flex items-center space-x-1">
            <span class="inline-block h-4 w-8 rounded-lg" style="background-color: {cat.color};"
            ></span>
            <span class="text-3xl font-bold text-gray-400">{cat.value}%</span>
            <span class="text-base text-gray-400">{cat.label}</span>
          </div>
        {/each}
      </div>
    </div>
  </Card.Content>
</Card.Root>
