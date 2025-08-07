<script lang="ts">
  import * as Select from '$lib/components/ui/select/index.js';

  interface Option {
    label: string;
    value: string;
    disabled?: boolean;
  }

  interface Props {
    options?: Option[];
    value?: string;
    placeholder?: string;
    class?: string;
    disabled?: boolean;
    label?: string;
    name?: string;
  }

  let {
    options = [
      { label: 'Pack', value: 'pack' },
      { label: 'Mentor', value: 'mentor' },
      { label: 'External', value: 'external' },
      { label: 'Internal', value: 'internal' },
      { label: 'Partner', value: 'partner' }
    ],
    value = $bindable(''),
    placeholder = 'Select option',
    class: className = 'w-[180px]',
    disabled = false,
    label = 'Options',
    name = 'select'
  }: Props = $props();

  const triggerContent = $derived(options.find(o => o.value === value)?.label ?? placeholder);
</script>

<Select.Root type="single" {name} bind:value {disabled}>
  <Select.Trigger class={className}>
    {triggerContent}
  </Select.Trigger>
  <Select.Content>
    <Select.Group>
      <Select.Label>{label}</Select.Label>
      {#each options as option (option.value)}
        <Select.Item value={option.value} label={option.label} disabled={option.disabled}>
          {option.label}
        </Select.Item>
      {/each}
    </Select.Group>
  </Select.Content>
</Select.Root>
