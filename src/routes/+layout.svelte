<script>
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav
	class="flex items-center space-x-6 bg-white px-6 py-4 text-sm font-medium text-gray-700 shadow-md"
>
	<a
		href="/"
		class="rounded-md bg-red-300 px-4 py-2 font-semibold text-white shadow transition hover:bg-red-400"
	>
		Create New
	</a>
	<a href="/history" class="transition hover:text-blue-600">History</a>
</nav>

{@render children?.()}
