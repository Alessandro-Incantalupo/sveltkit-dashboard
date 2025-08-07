<script lang="ts">
  import * as Select from '$lib/components/ui/select/index.js';

  interface Provider {
    label: string;
    value: string;
    disabled?: boolean;
  }

  interface Props {
    providers?: Provider[];
    value?: string;
    placeholder?: string;
    class?: string;
    disabled?: boolean;
  }

  let {
    providers = [
      { label: 'Pack', value: 'pack' },
      { label: 'Mentor', value: 'mentor' },
      { label: 'External', value: 'external' },
      { label: 'Internal', value: 'internal' },
      { label: 'Partner', value: 'partner' }
    ],
    value = $bindable(''),
    placeholder = 'Select provider',
    class: className = 'w-[180px]',
    disabled = false
  }: Props = $props();

  const triggerContent = $derived(providers.find(p => p.value === value)?.label ?? placeholder);
</script>

<Select.Root type="single" name="provider" bind:value {disabled}>
  <Select.Trigger class={className}>
    {triggerContent}
  </Select.Trigger>
  <Select.Content>
    <Select.Group>
      <Select.Label>Providers</Select.Label>
      {#each providers as provider (provider.value)}
        <Select.Item value={provider.value} label={provider.label} disabled={provider.disabled}>
          {provider.label}
        </Select.Item>
      {/each}
    </Select.Group>
  </Select.Content>
</Select.Root>
