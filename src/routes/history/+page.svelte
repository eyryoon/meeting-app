<script>
	import Avatar from 'svelte-boring-avatars';
	let meetings = $state([]);
	$effect(() => {
		meetings = JSON.parse(localStorage.getItem('meetings') || '[]');
	});
</script>

<div class="rounded-lg p-8">
	<section class="py-8 text-center">
		<h1 class="text-4xl leading-tight font-extrabold text-sky-600">your meetings</h1>
		<p class="mx-auto mt-3 max-w-2xl text-gray-600">
			{#if meetings.length === 0}
				no meetings yet - <a href="/" class="text-sky-500 underline hover:text-sky-700"
					>create your first one!</a
				>
			{:else}
				here are all your past and current meetings
			{/if}
		</p>
	</section>

	{#if meetings.length > 0}
		<section class="mx-auto max-w-4xl space-y-4">
			{#each meetings as meeting}
				<div
					class="rounded-xl border border-gray-100 bg-white p-6 shadow-lg transition-shadow hover:shadow-xl"
				>
					<div class="flex items-center justify-between">
						<div class="flex-1">
							<h3 class="mb-2 text-xl font-bold text-sky-600">{meeting.name}</h3>
							<div class="space-y-1 text-sm text-gray-600">
								<p>Meeting ID: <span class="font-mono text-sky-500">{meeting.id}</span></p>
								<p>Created: {new Date(meeting.created || Date.now()).toLocaleDateString()}</p>
								<p class="flex items-center gap-2">
									<span class="inline-flex items-center gap-1">
										<span class="h-2 w-2 rounded-full bg-green-400"></span>
										{meeting.submissions.length} participants
									</span>
								</p>
							</div>
						</div>

						{#if meeting.submissions.length > 0}
							<div class="mr-4 flex -space-x-2">
								{#each meeting.submissions.slice(0, 5) as participant}
									<div class="rounded-full ring-2 ring-white">
										<Avatar size={40} name={participant.name} variant="beam" />
									</div>
								{/each}
								{#if meeting.submissions.length > 5}
									<div
										class="flex h-10 w-10 items-center justify-center rounded-full bg-gray-200 text-xs font-semibold text-gray-600 ring-2 ring-white"
									>
										+{meeting.submissions.length - 5}
									</div>
								{/if}
							</div>
						{/if}

						<div class="flex gap-2">
							<a
								href={`/meeting/${meeting.id}/results`}
								class="inline-flex items-center gap-1 rounded-md bg-sky-500 px-3 py-2 text-sm font-semibold text-white transition hover:bg-sky-600"
							>
								View Results
							</a>
							<a
								href={`/meeting/${meeting.id}`}
								class="inline-flex items-center gap-1 rounded-md border border-gray-300 bg-white px-3 py-2 text-sm font-semibold text-gray-700 transition hover:bg-gray-50"
							>
								Join Meeting
							</a>
						</div>
					</div>
				</div>
			{/each}
		</section>

		<section class="mx-auto mt-8 max-w-4xl text-center">
			<a
				href="/"
				class="inline-flex items-center gap-2 rounded-md bg-sky-500 px-6 py-3 font-semibold text-white transition hover:bg-sky-600"
			>
				Create New Meeting
			</a>
		</section>
	{/if}
</div>
