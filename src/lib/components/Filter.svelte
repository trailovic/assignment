<script lang="ts">
    let { selected = $bindable<'All' | 'Active' | 'Completed'>('All') } = $props();

    const options = ['All', 'Active', 'Completed'] as const;
</script>

<div class="flex justify-center items-center gap-6 border-t-2 border-b-2 w-screen lg:w-1/3">
    {#each options as option}
        <button
            class="px-3 py-1.5 border-none cursor-pointer {
                selected === option ? 'bg-[var(--primary-500)] text-white' : 'hover:bg-[var(--primary-100)]'
            }"
            
            onclick={() => selected = option}
        >
            {option}
        </button>
    {/each}
</div>