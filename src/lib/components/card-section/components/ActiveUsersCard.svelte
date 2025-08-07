<script lang="ts">
  import * as Card from '$lib/components/ui/card/index.js';
  import * as Chart from 'chart.js';
  import { onMount } from 'svelte';
  export let percentage: number;

  let canvas: HTMLCanvasElement;
  let chart: Chart.Chart;

  onMount(() => {
    Chart.Chart.register(...Chart.registerables);
    chart = new Chart.Chart(canvas, {
      type: 'doughnut',
      data: {
        datasets: [
          {
            data: [percentage, 100 - percentage],
            backgroundColor: ['#3b82f6', '#e5e7eb'],
            borderWidth: 0
          }
        ]
      },
      options: {
        circumference: 270,
        rotation: -135,
        responsive: true,
        maintainAspectRatio: true,
        cutout: '75%',
        plugins: {
          legend: { display: false },
          tooltip: { enabled: false }
        }
      }
    });
  });
</script>

<Card.Root class="flex flex-col items-center justify-center px-12 py-4">
  <Card.Content class="flex flex-col items-center space-y-6 text-center">
    <div class="relative h-52 w-52">
      <canvas bind:this={canvas} class="h-52 w-52"></canvas>
      <div class="pointer-events-none absolute inset-0 flex items-center justify-center">
        <span class="text-5xl font-bold text-blue-500">{percentage}%</span>
      </div>
    </div>
    <div class="space-y-2">
      <h3 class="text-lg font-medium text-gray-900">Active Users</h3>
      <p class="text-base text-gray-500">Access Rate</p>
    </div>
  </Card.Content>
</Card.Root>
