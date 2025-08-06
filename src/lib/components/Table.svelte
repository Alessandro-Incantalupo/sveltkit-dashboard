<!-- filepath: src/lib/components/Table.svelte -->
<script lang="ts">
  export let data: Array<{
    title: string;
    path: string;
    views: number;
    uploadedBy: string;
    provider: string;
    type: string;
  }>;
</script>

<table class="w-full border-collapse border border-gray-200">
  <thead>
    <tr class="bg-gray-50">
      <th class="border px-4 py-2 text-left">Content Title</th>
      <th class="border px-4 py-2 text-left">Path</th>
      <th class="border px-4 py-2 text-left">View Count</th>
      <th class="border px-4 py-2 text-left">Uploaded By</th>
      <th class="border px-4 py-2 text-left">Provider</th>
      <th class="border px-4 py-2 text-left">Type</th>
    </tr>
  </thead>
  <tbody>
    {#each data as row}
      <tr class="hover:bg-gray-100">
        <td class="border px-4 py-2">{row.title}</td>
        <td class="border px-4 py-2">{row.path}</td>
        <td class="border px-4 py-2">{row.views}</td>
        <td class="border px-4 py-2">{row.uploadedBy}</td>
        <td class="border px-4 py-2">{row.provider}</td>
        <td class="border px-4 py-2">{row.type}</td>
      </tr>
    {/each}
  </tbody>
</table>
