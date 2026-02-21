<script lang="ts">
  import { Button } from "$lib/components/ui/button/index.js";
  import Send from "$lib/assets/send.svg";
</script>

<div class="w-1/3 flex items-center justify-between border-2 rounded-full px-2 py-1">
    <input 
      type="text" 
      placeholder="Add a new task..." 
      class="w-full p-2 outline-none" 
    />
    <Button class="rounded-full h-14 bg-[var(--primary-500)] hover:bg-[var(--primary-600)] cursor-pointer">
      <img src={Send} alt="Send" class="w-6 h-6" />
    </Button>
</div>