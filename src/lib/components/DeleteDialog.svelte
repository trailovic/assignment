<script lang="ts">
    import {
        Dialog,
        DialogContent,
        DialogDescription,
        DialogFooter,
        DialogHeader,
        DialogTitle,
    } from "$lib/components/ui/dialog/index.js";
    import { Button } from "$lib/components/ui/button/index.js";

    let { open = $bindable(false), onDelete }: { open: boolean, onDelete: () => void } = $props();
</script>

<Dialog bind:open>
    <DialogContent>
        <DialogHeader>
            <DialogTitle>Delete Task</DialogTitle>
            <DialogDescription>
                Are you sure you want to delete this task? This action cannot be undone.
            </DialogDescription>
        </DialogHeader>
        <DialogFooter>
            <Button variant="outline" onclick={() => open = false} class="cursor-pointer">Cancel</Button>
            <Button variant="destructive" onclick={onDelete} class="cursor-pointer hover:bg-[var(--600)]">Delete</Button>
        </DialogFooter>
    </DialogContent>
</Dialog>