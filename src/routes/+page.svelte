<script>
	import { onMount } from 'svelte';

	let meetingName = '';
	let error = '';

	function createMeeting() {
		error = '';
		const name = meetingName.trim();
		if (!name) {
			error = 'Please enter a meeting name.';
			return;
		}

		const raw = localStorage.getItem('meetings');
		const meetings = raw ? JSON.parse(raw) : [];

		const meeting = {
			id: Date.now().toString(36),
			name,
			submissions: [],
			created: new Date()
		};

		localStorage.setItem('meetings', JSON.stringify([...meetings, meeting]));

		// navigate to /new and attach the created meeting id in sessionStorage for the new page to pick up
		sessionStorage.setItem('editingMeetingId', meeting.id);
		window.location.href = '/new/' + meeting.id;
	}

	// small UX: focus input on mount
	let nameInput;
	onMount(() => nameInput?.focus());
</script>

<div class="rounded-lg p-8">
	<section class="py-12 text-center">
		<h1 class="text-5xl leading-tight font-extrabold text-sky-600">replace with your own text</h1>
		<p class="mx-auto mt-4 max-w-2xl text-gray-600">replace this with your own text</p>
		<p class="mx-auto mt-4 max-w-2xl text-gray-600">
			Quick note from Daniel: The functionality now works. So create a link, and visit the link
			multiple times and submit with different names to fill up the scheduler!
		</p>
	</section>

	<section class="mx-auto max-w-md rounded-xl border border-gray-100 bg-white p-6 shadow-lg">
		<label for="meeting-name" class="text-sm font-medium text-gray-700">Meeting name</label>
		<input
			id="meeting-name"
			bind:this={nameInput}
			bind:value={meetingName}
			type="text"
			placeholder="e.g. Weekly retro — Oct 18"
			class="mt-2 w-full rounded-md border border-gray-200 px-4 py-2 text-sm focus:ring-2 focus:ring-sky-200 focus:outline-none"
			on:keydown={(e) => e.key === 'Enter' && createMeeting()}
		/>

		{#if error}
			<div class="mt-3 text-sm text-red-600">{error}</div>
		{/if}

		<div class="mt-6 flex justify-end">
			<button
				class="inline-flex items-center gap-2 rounded-md bg-sky-500 px-4 py-2 font-semibold text-white transition hover:bg-sky-600"
				on:click={createMeeting}
			>
				Create Meeting
			</button>
		</div>
	</section>
</div>
