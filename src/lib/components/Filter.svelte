<script>
    let selected = 'All';

    const options = ['All', 'Active', 'Completed'];
</script>

<div class="flex justify-center items-center gap-6 border-t-2 border-b-2 w-1/3 py-1">
    {#each options as option}
        <button
            class="px-3 py-1.5 rounded-full border-none cursor-pointer {
                selected === option ? 'bg-[var(--primary-500)] text-white' : 'hover:bg-[var(--primary-100)]'
            }"
            
            on:click={() => selected = option}
        >
            {option}
        </button>
    {/each}
</div>