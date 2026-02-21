<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import Send from "$lib/assets/send.svg";

  let { onAdd }: { onAdd: (text: string) => void } = $props();
  let inputValue = $state("");
  let showError = $state(false);

  function handleAdd() {
    if (inputValue.trim()) {
      onAdd(inputValue.trim());
      inputValue = "";
      showError = false;
    } else {
      showError = true;
    }
  }

  function handleInput() {
    if (showError && inputValue.trim()) {
      showError = false;
    }
  }
</script>

<div class="w-full lg:w-1/3 flex flex-col gap-1">
  {#if showError}
    <span class="text-sm text-red-500 pl-4">Please enter task name</span>
  {/if}
  <div class="flex items-center justify-between border-2 rounded-full px-2 py-1">
      <input 
        type="text" 
        placeholder="Add a new task..." 
        class="w-full p-2 outline-none"
        bind:value={inputValue}
        oninput={handleInput}
        onkeydown={(e) => e.key === 'Enter' && handleAdd()}
      />
      <Button 
        class="rounded-full h-14 bg-[var(--primary-500)] hover:bg-[var(--primary-600)] cursor-pointer"
        onclick={handleAdd}
      >
        <img src={Send} alt="Send" class="w-6 h-6" />
      </Button>
  </div>
</div>