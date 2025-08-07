<script lang="ts">
  import * as Card from '$lib/components/ui/card/index.js';
  import * as Chart from 'chart.js';
  import { onMount } from 'svelte';

  let canvas: HTMLCanvasElement;
  let chart: Chart.Chart;

  let labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
  let uploadedData = [200, 300, 400, 350, 500, 600, 700, 650, 800, 900, 950, 1100];
  let usageData = [180, 250, 370, 320, 480, 700, 670, 600, 780, 850, 900, 1000];

  const handleResize = () => {
    if (chart) {
      setTimeout(() => {
        chart.resize();
      }, 100);
    }
  };

  onMount(() => {
    Chart.Chart.register(...Chart.registerables);
    chart = new Chart.Chart(canvas, {
      type: 'line',
      data: {
        labels,
        datasets: [
          {
            label: 'Uploaded Content',
            data: uploadedData,
            borderColor: '#2b6cb0',
            backgroundColor: 'rgba(43, 108, 176, 0.1)',
            tension: 0.4,
            fill: false
          },
          {
            label: 'Usage',
            data: usageData,
            borderColor: '#ed8936',
            backgroundColor: 'rgba(237, 137, 54, 0.1)',
            tension: 0.4,
            fill: false
          }
        ]
      },
      options: {
        responsive: true,
        plugins: {
          legend: { display: false },
          tooltip: { enabled: true }
        },
        scales: {
          y: { beginAtZero: true }
        }
      }
    });
    window.addEventListener('resize', handleResize);

    return () => {
      window.removeEventListener('resize', handleResize);
    };
  });
</script>

<Card.Root class="flex flex-col items-center justify-center px-8 py-6">
  <Card.Content class="w-full text-center">
    <h3 class="mb-2 text-sm font-semibold text-gray-700">Uploaded content vs Usage over time</h3>
    <div class="w-full">
      <canvas bind:this={canvas} height="200"></canvas>
    </div>
  </Card.Content>
</Card.Root>
