<script>
    import Title from '$lib/components/Title.svelte';
    import Filter from '$lib/components/Filter.svelte';
    import Empty from '$lib/components/Empty.svelte';
    import Tasks from '$lib/components/Tasks.svelte';
    import Input from '$lib/components/Input.svelte';
</script>

<main class="w-screen h-screen flex flex-col items-center justify-between gap-6 p-4 pt-16">
    <Title />
    <Filter />
    <Empty />
    <Tasks />
    <Input />
</main>