<script lang="ts">
    import {
        Dialog,
        DialogContent,
        DialogFooter,
        DialogHeader,
        DialogTitle,
    } from "$lib/components/ui/dialog/index.js";
    import { Button } from "$lib/components/ui/button/index.js";
    import EditDark from "$lib/assets/edit_dark.svg";

    let { open = $bindable(false), taskText, onSave }: { open: boolean, taskText: string, onSave: (newText: string) => void } = $props();
    let editMode = $state(false);
    let editedText = $state("");

    function startEdit() {
        editedText = taskText;
        editMode = true;
    }

    function cancelEdit() {
        editMode = false;
        editedText = "";
    }

    function saveEdit() {
        if (editedText.trim()) {
            onSave(editedText.trim());
        }
        editMode = false;
        editedText = "";
        open = false;
    }

    function handleCancel() {
        cancelEdit();
        open = false;
    }

    $effect(() => {
        if (!open) {
            editMode = false;
            editedText = "";
        }
    });
</script>

<Dialog bind:open>
    <DialogContent>
        <DialogHeader>
            <DialogTitle>Edit Task</DialogTitle>
        </DialogHeader>

        {#if !editMode}
            <div class="py-4 flex items-center justify-start gap-2">
                <span class="text-lg">{taskText}</span>
                <Button variant="ghost" onclick={startEdit} class="cursor-pointer">
                    <img src={EditDark} alt="Edit" class="w-5 h-5" />
                </Button>
            </div>
            <DialogFooter>
                <Button variant="outline" onclick={handleCancel} class="cursor-pointer">Cancel</Button>
            </DialogFooter>
        {:else}
            <div class="py-4 flex flex-col gap-4">
                <span class="text-sm text-[var(--neutral-500)]">{taskText}</span>
                <input 
                    type="text" 
                    bind:value={editedText}
                    class="w-full p-2 border-2 rounded-md outline-none focus:border-[var(--primary-500)]"
                />
            </div>
            <DialogFooter>
                <Button variant="outline" onclick={cancelEdit} class="cursor-pointer">Cancel</Button>
                <Button onclick={saveEdit} class="cursor-pointer bg-[var(--primary-500)] hover:bg-[var(--primary-600)]">Save</Button>
            </DialogFooter>
        {/if}
    </DialogContent>
</Dialog>