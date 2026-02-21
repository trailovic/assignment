<script lang="ts">
    import {
        DropdownMenu,
        DropdownMenuContent,
        DropdownMenuItem,
        DropdownMenuTrigger,
    } from "$lib/components/ui/dropdown-menu/index.js";
    import MoreHorizontal from "$lib/assets/more_button.svg";
    import Edit from "$lib/assets/edit.svg";
    import Delete from "$lib/assets/delete.svg";
    import DeleteDialog from "./DeleteDialog.svelte";
    import EditDialog from "./EditDialog.svelte";

    let { taskId, taskText, onDelete, onEdit }: { taskId: number, taskText: string, onDelete: (id: number) => void, onEdit: (id: number, newText: string) => void } = $props();
    let showDeleteDialog = $state(false);
    let showEditDialog = $state(false);

    function handleDelete() {
        onDelete(taskId);
        showDeleteDialog = false;
    }

    function handleEdit(newText: string) {
        onEdit(taskId, newText);
        showEditDialog = false;
    }
</script>

<DropdownMenu>
    <DropdownMenuTrigger class="cursor-pointer">
        <img src={MoreHorizontal} alt="More" class="w-5 h-5" />
    </DropdownMenuTrigger>
    <DropdownMenuContent>
        <DropdownMenuItem class="flex items-center justify-between" onclick={() => showEditDialog = true}>
            <span>Edit Task</span>
            <img src={Edit} alt="Edit" class="w-5" />
        </DropdownMenuItem>
        <DropdownMenuItem class="flex items-center justify-between" onclick={() => showDeleteDialog = true}>
            <span>Delete Task</span>
            <img src={Delete} alt="Delete" class="w-5" />
        </DropdownMenuItem>
    </DropdownMenuContent>
</DropdownMenu>

<DeleteDialog bind:open={showDeleteDialog} onDelete={handleDelete} />
<EditDialog bind:open={showEditDialog} taskText={taskText} onSave={(newText) => handleEdit(newText)} />