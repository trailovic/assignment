<script lang="ts">
 import { Checkbox } from "$lib/components/ui/checkbox/index.js";
</script>

<div class="flex flex-col justify-start items-start w-1/3 h-full">
    <div class="flex items-center gap-4 w-full">
        <Checkbox class="size-10" />
        <span class="text-xl gap-y-4">Example Active Task</span>
    </div>

    <span class="w-full border-t-2 my-6"></span>

    <div class="flex items-center gap-4 w-full">
        <Checkbox class="size-10" />
        <span class="text-xl text-[var(--neutral-500)] font-light gap-y-4">Example Completed Task</span>
    </div>
</div>