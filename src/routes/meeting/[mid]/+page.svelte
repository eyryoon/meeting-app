<script>
	import { goto } from '$app/navigation';
	const p = $props();
	const mid = p.params.mid;

	const DAYS = 'Sun,Mon,Tue,Wed,Thu,Fri,Sat'.split(',');
	let arr = $state(new Array(105).fill(false));
	let participantName = $state('');

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

		console.log('mid', mid);
		console.log('meetings 1', meetings);
		meetings = meetings.map((m) =>
			m.id === mid ? { ...m, submissions: [...m.submissions, submission] } : m
		);
		console.log('meetings 2', meetings);

		localStorage.setItem('meetings', JSON.stringify(meetings));
		goto(`/meeting/${mid}/results`);
	}
</script>

<div class="rounded-lg p-8">
	<section class="py-8 text-center">
		<h1 class="text-4xl leading-tight font-extrabold text-sky-600">when works for you?</h1>
		<p class="mx-auto mt-3 max-w-2xl text-gray-600">
			meeting: <span class="font-semibold text-sky-600">{mid}</span>
		</p>
	</section>

	<section class="mx-auto max-w-4xl rounded-xl border border-gray-100 bg-white p-6 shadow-lg">
		<div class="mb-6">
			<label for="participant-name" class="text-sm font-medium text-gray-700">Your name</label>
			<input
				id="participant-name"
				type="text"
				placeholder="Enter your name here"
				bind:value={participantName}
				class="mt-2 w-full max-w-md rounded-md border border-gray-200 px-4 py-2 text-sm focus:ring-2 focus:ring-sky-200 focus:outline-none"
			/>
		</div>

		<div class="mb-4">
			<p class="mb-3 text-sm font-medium text-gray-700">Select your available times:</p>

			<div class="rounded-lg bg-gray-50 p-4">
				<div class="mb-2 grid grid-cols-7 text-center text-sm font-semibold text-gray-700">
					{#each DAYS as day}
						<div class="py-2">{day}</div>
					{/each}
				</div>

				<div class="grid grid-cols-7 gap-px rounded bg-gray-200">
					{#each arr as v, i}
						<button
							class="flex h-10 cursor-pointer items-center justify-center text-xs transition-colors"
							class:bg-sky-200={v}
							class:bg-white={!v}
							class:hover:bg-sky-100={v}
							class:hover:bg-sky-50={!v}
							class:text-gray-400={!v}
							class:text-sky-700={v}
							onclick={() => (arr[i] = !arr[i])}
						>
							{toAmPm(Math.floor(i / 7) + 8)}
						</button>
					{/each}
				</div>
			</div>
		</div>

		<div class="mt-6 flex justify-end gap-3">
			<a
				href="/"
				class="inline-flex items-center gap-2 rounded-md border border-gray-300 bg-white px-4 py-2 font-semibold text-gray-700 transition hover:bg-gray-50"
			>
				Back Home
			</a>

			<button
				onclick={addSubmission}
				class="inline-flex items-center gap-2 rounded-md bg-sky-500 px-6 py-2 font-semibold text-white transition hover:bg-sky-600"
				disabled={!participantName.trim()}
			>
				Submit Availability
			</button>
		</div>
	</section>
</div>
