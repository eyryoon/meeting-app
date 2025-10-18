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

<div class="space-y-2">
	{#each [1, 2, 3] as v}
		<div class="flex items-center rounded-xl bg-gray-400 p-2">
			<div class="bg-pink-300">*</div>
			<div class="flex-1 bg-green-200">
				<div>[group name...] [code #]</div>
				<div>10/2</div>
				<div>Met <input type="checkbox" /></div>
			</div>
			<div>
				<div class="bg-pink-300">avatars</div>
			</div>
		</div>
	{/each}
</div>
