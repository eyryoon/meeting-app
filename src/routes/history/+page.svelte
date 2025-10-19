<script>
	let data = [
		{
			name: 'study group',
			code: '',
			date: '',
			participants: ['james'],
			completed: false
		},
		{
			name: 'pool party',
			code: '',
			date: '',
			participants: [],
			completed: true
		}
	];
</script>

<div class="mt-4 space-y-5">
	{#each [1, 2, 3] as v}
		<div
			class="hover-shadow-lg flex cursor-pointer items-center rounded-xl border border-gray-500 p-2"
		>
			<div class="bg-pink-300">*</div>
			<div class="flex-1">
				<div><span class="bold-text text-2xl">[group name...]</span> [code #]</div>
				<div class="mt-2">Created 10/2</div>
				<div>Met <input type="checkbox" /></div>
			</div>
			<div>
				<div class="bg-pink-300">avatars</div>
			</div>
		</div>
	{/each}
</div>
