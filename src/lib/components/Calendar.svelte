<script lang="ts">
  import { buttonVariants } from '$lib/components/ui/button/index.js';
  import { Calendar } from '$lib/components/ui/calendar/index.js';
  import * as Popover from '$lib/components/ui/popover/index.js';
  import { cn } from '$lib/utils.js';
  import { DateFormatter, type DateValue, getLocalTimeZone } from '@internationalized/date';
  import CalendarIcon from '@lucide/svelte/icons/calendar';

  const df = new DateFormatter('it-IT', {
    dateStyle: 'long'
  });

  let value = $state<DateValue | undefined>();
  let contentRef = $state<HTMLElement | null>(null);
</script>

<Popover.Root>
  <Popover.Trigger
    class={cn(
      buttonVariants({
        variant: 'outline',
        class: 'w-[280px] basis-1/3 justify-between text-left font-normal'
      }),
      !value && 'text-muted-foreground'
    )}
  >
    {value ? df.format(value.toDate(getLocalTimeZone())) : 'Pick a date'}
    <CalendarIcon />
  </Popover.Trigger>
  <Popover.Content bind:ref={contentRef} class="w-auto p-0">
    <Calendar type="single" bind:value />
  </Popover.Content>
</Popover.Root>
