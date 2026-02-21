<script lang="ts">
    import Title from '$lib/components/Title.svelte';
    import Filter from '$lib/components/Filter.svelte';
    import Empty from '$lib/components/Empty.svelte';
    import Tasks from '$lib/components/Tasks.svelte';
    import Input from '$lib/components/Input.svelte';
    import { Toaster } from '$lib/components/ui/sonner/index.js';
    import { toast } from 'svelte-sonner';

    interface Task {
        id: number;
        text: string;
        completed: boolean;
    }

    let tasks = $state<Task[]>([]);
    let idCounter = $state(0);
    let filter = $state<'All' | 'Active' | 'Completed'>('All');

    let filteredTasks = $derived(
        filter === 'All' ? tasks :
        filter === 'Active' ? tasks.filter(t => !t.completed) :
        tasks.filter(t => t.completed)
    );

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
        toast.success('Task created');
    }

    function toggleTask(id: number) {
        tasks = tasks.map(t => t.id === id ? { ...t, completed: !t.completed } : t);
    }

    function deleteTask(id: number) {
        tasks = tasks.filter(t => t.id !== id);
        toast.success('Task deleted');
    }

    function editTask(id: number, newText: string) {
        tasks = tasks.map(t => t.id === id ? { ...t, text: newText } : t);
        toast.success('Task edited');
    }
</script>

<main class="w-screen h-screen flex flex-col items-center justify-between gap-6 p-4 pt-16">
    <Title />
    <Filter bind:selected={filter} />
    {#if filteredTasks.length === 0}
    <Empty />
    {:else}
    <Tasks tasks={filteredTasks} onToggle={toggleTask} onDelete={deleteTask} onEdit={editTask} />
    {/if}
    <Input onAdd={addTask} />
    <Toaster />
</main>