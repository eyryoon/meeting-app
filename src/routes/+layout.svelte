<script>
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	// keep favicon import; layout will use <slot /> for routing content
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="flex min-h-screen flex-col bg-slate-50">
	<header class="bg-white/80 shadow-sm backdrop-blur-sm">
		<div class="mx-auto flex max-w-4xl items-center justify-between px-6 py-4">
			<a href="/" class="flex items-center gap-3">
				<span class="text-lg font-extrabold text-sky-600">Meeting Scheduler</span>
			</a>

			<nav class="flex items-center gap-4 text-sm text-gray-700">
				<a
					href="/"
					class="hidden rounded-md bg-sky-500 px-4 py-2 font-semibold text-white shadow transition hover:bg-sky-600 sm:inline-block"
				>
					Create New
				</a>
				<a href="/history" class="rounded px-2 py-1 transition hover:bg-gray-100">History</a>
			</nav>
		</div>
	</header>

	<main class="flex-grow">
		<div class="mx-auto max-w-4xl px-6 py-10">
			<slot />
		</div>
	</main>
</div>
