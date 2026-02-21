<script lang="ts">
    import Title from '$lib/components/Title.svelte';
    import Filter from '$lib/components/Filter.svelte';
    import Empty from '$lib/components/Empty.svelte';
    import Tasks from '$lib/components/Tasks.svelte';
    import Input from '$lib/components/Input.svelte';

    interface Task {
        id: number;
        text: string;
        completed: boolean;
    }

    let tasks = $state<Task[]>([]);
    let idCounter = $state(0);

    $effect(() => {
        const saved = localStorage.getItem('tasks');
        if (saved) {
            const parsed = JSON.parse(saved);
            tasks = parsed.tasks;
            idCounter = parsed.idCounter;
        }
    });

    $effect(() => {
        localStorage.setItem('tasks', JSON.stringify({ tasks, idCounter }));
    });

    function addTask(text: string) {
        tasks = [...tasks, { id: idCounter++, text, completed: false }];
    }

    function toggleTask(id: number) {
        tasks = tasks.map(t => t.id === id ? { ...t, completed: !t.completed } : t);
    }
</script>

<main class="w-screen h-screen flex flex-col items-center justify-between gap-6 p-4 pt-16">
    <Title />
    <Filter />
    {#if tasks.length === 0}
    <Empty />
    {:else}
    <Tasks {tasks} onToggle={toggleTask} />
    {/if}
    <Input onAdd={addTask} />
</main>