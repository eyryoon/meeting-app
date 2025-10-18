<script>
	const p = $props();
	const mid = p.params.mid;

	const DAYS = 'Sun,Mon,Tue,Wed,Thu,Fri,Sat'.split(',');
	let arr = $state(new Array(105).fill(false));
	let participantName = '';

	function toAmPm(hr) {
		if (hr <= 11) return hr + 'AM';
		else if (hr == 12) return hr + 'PM';
		else return hr - 12 + 'PM';
	}

	function addSubmission() {
		let meetings = JSON.parse(localStorage.getItem('meetings'));

		let submission = {
			name: participantName,
			submission: arr
		};
		meetings = meetings.map((m) =>
			m.name === mid ? { ...m, submissions: [...m.submissions, submission] } : m
		);
		localStorage.setItem('meetings', JSON.stringify(meetings));
	}
</script>

<div class="bg-blue-100 p-5 font-semibold">GROUP: {mid}</div>

<div class="mt-4 ml-2 flex items-center space-x-2">
	<span>Enter your name</span>
	<input
		type="text"
		placeholder="Type here"
		bind:value={participantName}
		class="rounded border border-gray-300 px-2 py-1 text-sm"
	/>
</div>

<div class="mt-6 mb-2 ml-2">Select which times you are available:</div>

<div class="mt-8 mb-1 grid grid-cols-7 text-center text-sm font-semibold text-gray-700">
	{#each DAYS as day}
		<div>{day}</div>
	{/each}
</div>

<div class="grid grid-cols-7">
	{#each arr as v, i}
		<button
			class="flex h-8 cursor-pointer items-center justify-center border border-gray-100 text-xs hover:bg-blue-50"
			class:bg-blue-200={v}
			class:text-gray-300={!v}
			onclick={() => (arr[i] = !arr[i])}
		>
			{toAmPm(Math.floor(i / 7) + 8)}
		</button>
	{/each}
</div>

<div class="mt-6 mr-2 flex justify-end">
	<a href={`/meeting/${mid}/results`}
		><button
			onclick={addSubmission}
			class="btn rounded-md bg-red-300 px-4 py-2 font-semibold text-white shadow transition hover:bg-red-400"
			>Submit</button
		></a
	>
</div>
