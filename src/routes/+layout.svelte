<script>
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav class="bg-white shadow-md px-6 py-4 flex space-x-6 items-center text-sm font-medium text-gray-700">
	<a href="/" class="bg-red-300 text-white px-4 py-2 rounded-md shadow hover:bg-red-400 transition font-semibold">
		Create New
	</a>
	<a href="/new" class="hover:text-blue-600 transition">Share</a>
</nav>

{@render children?.()}
