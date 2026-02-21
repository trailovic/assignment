<script lang="ts">
 import { Checkbox } from "$lib/components/ui/checkbox/index.js";
 import TaskDropdown from "./TaskDropdown.svelte";

 interface Task {
    id: number;
    text: string;
    completed: boolean;
 }

 let { tasks = [], onToggle, onDelete, onEdit }: { tasks: Task[], onToggle: (id: number) => void, onDelete: (id: number) => void, onEdit: (id: number, newText: string) => void } = $props();

 let activeTasks = $derived(tasks.filter(t => !t.completed));
 let completedTasks = $derived(tasks.filter(t => t.completed));
</script>

<div class="flex flex-col justify-start items-start w-1/3 h-full pt-6">
    {#each activeTasks as task (task.id)}
    <div class="flex items-center justify-between w-full mb-4">
            <div class="flex items-center w-full gap-x-4">
                <Checkbox class="size-10" checked={task.completed} onCheckedChange={() => onToggle(task.id)} />
                <span class="text-xl gap-y-4">{task.text}</span>
            </div>
            <div>
                <TaskDropdown taskId={task.id} taskText={task.text} {onDelete} {onEdit} />
            </div>
        </div>
    {/each}

    {#if activeTasks.length > 0 && completedTasks.length > 0}
    <span class="w-full border-t-2 my-6"></span>
    {/if}

    {#each completedTasks as task (task.id)}
        <div class="flex items-center justify-between w-full mb-4">
            <div class="flex items-center w-full gap-x-4">
                <Checkbox class="size-10" checked={task.completed} onCheckedChange={() => onToggle(task.id)} />
                <span class="text-xl text-[var(--neutral-500)] font-light gap-y-4">{task.text}</span>
            </div>
            <div>
                <TaskDropdown taskId={task.id} taskText={task.text} {onDelete} {onEdit} />
            </div>
        </div>
    {/each}
</div>