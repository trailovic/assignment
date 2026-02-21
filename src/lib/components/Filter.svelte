<script>
    let selected = 'All';

    const options = ['All', 'Active', 'Completed'];
</script>

<div class="flex gap-2">
    {#each options as option}
        <button
            class="px-3 py-1.5 rounded text-sm border-none cursor-pointer {
                selected === option ? 'bg-purple-700 text-white' : ''
            }" 
            
            on:click={() => selected = option}
        >
            {option}
        </button>
    {/each}
</div>