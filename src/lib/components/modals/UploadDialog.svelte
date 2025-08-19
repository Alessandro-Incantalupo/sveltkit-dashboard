<script lang="ts">
  import SelectForm from '$lib/components/forms/SelectForm.svelte';
  import { Button } from '$lib/components/ui/button';
  import * as Dialog from '$lib/components/ui/dialog/index.js';
  import { Input } from '$lib/components/ui/input';

  interface Props {
    open?: boolean;
    uploadTitle?: string;
    uploadDescription?: string;
    uploadCategory?: string;
    uploadLanguage?: string;
    uploadProvider?: string;
    uploadRole?: string;
    categoryOptions: Array<{ label: string; value: string }>;
    languageOptions: Array<{ label: string; value: string }>;
    providerOptions: Array<{ label: string; value: string }>;
    roleOptions: Array<{ label: string; value: string }>;
    onSubmit?: () => void;
  }

  let {
    open = $bindable(false),
    uploadTitle = $bindable(''),
    uploadDescription = $bindable(''),
    uploadCategory = $bindable(''),
    uploadLanguage = $bindable(''),
    uploadProvider = $bindable(''),
    uploadRole = $bindable(''),
    categoryOptions,
    languageOptions,
    providerOptions,
    roleOptions,
    onSubmit = () => {}
  }: Props = $props();

  function handleSubmitUpload() {
    onSubmit();
  }
</script>

<!-- Upload Dialog -->
<Dialog.Root bind:open>
  <Dialog.Content class="sm:max-w-[500px]">
    <Dialog.Header>
      <Dialog.Title>Upload Resource</Dialog.Title>
    </Dialog.Header>
    <div class="grid gap-4 py-4">
      <Input id="title" bind:value={uploadTitle} placeholder="Title*" />
      <Input id="description" bind:value={uploadDescription} placeholder="Description*" />

      <SelectForm
        bind:value={uploadCategory}
        options={categoryOptions}
        placeholder="Category*"
        label="Categories"
        name="category"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadLanguage}
        options={languageOptions}
        placeholder="Language*"
        label="Languages"
        name="language"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadProvider}
        options={providerOptions}
        placeholder="Provider*"
        label="Providers"
        name="provider"
        class="w-full"
      />

      <SelectForm
        bind:value={uploadRole}
        options={roleOptions}
        placeholder="Role"
        label="Roles"
        name="role"
        class="w-full"
      />

      <div class="flex gap-3">
        <Input id="file" type="file" placeholder="No file selected*" class="flex-1" />
        <Button variant="outline" class="whitespace-nowrap">Select file</Button>
      </div>
    </div>
    <Dialog.Footer>
      <Button type="submit" onclick={handleSubmitUpload} class="bg-orange-500 hover:bg-orange-600"
        >Upload</Button
      >
    </Dialog.Footer>
  </Dialog.Content>
</Dialog.Root>
