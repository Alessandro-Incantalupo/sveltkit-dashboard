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
            backgroundColor: ['#f97316', '#e5e7eb'], // orange and gray
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

<Card.Root class="flex min-h-[300px] flex-col items-center justify-center px-8 py-6">
  <Card.Content class="flex flex-col items-center space-y-4 text-center">
    <div class="relative h-40 w-40">
      <canvas bind:this={canvas} class="h-40 w-40"></canvas>
      <div class="pointer-events-none absolute inset-0 flex items-center justify-center">
        <span class="text-3xl font-bold text-orange-500">{percentage}%</span>
      </div>
    </div>
    <div class="space-y-1">
      <h3 class="text-lg font-medium text-gray-900">Resources</h3>
      <p class="text-sm text-gray-500">Utilized</p>
    </div>
  </Card.Content>
</Card.Root>
