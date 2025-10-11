<script>
	import { onMount } from 'svelte';
	import Avatar from 'svelte-boring-avatars';

	let showPopup = $state(undefined);

	const p = $props();
	// const mid = p.params.mid;
	const mid = 'study group';
	let participants = $state([]);
    let maxIndex = $state(-1);

	onMount(() => {
		let meetings = localStorage.getItem('meetings');

		if (meetings === null) return;

		meetings = JSON.parse(meetings);

		let meeting = meetings.find((m) => m.name === mid);

		participants = meeting.submissions;
		console.log(participants);

        getMaxIndex();
	});

	const DAYS = 'Sun,Mon,Tue,Wed,Thu,Fri,Sat'.split(',');
	let arr = new Array(105).fill(false);

	function toAmPm(hr) {
		if (hr <= 11) return hr + 'AM';
		else if (hr == 12) return hr + 'PM';
		else return hr - 12 + 'PM';
	}

	function getBorderClasses(submission) {
		if (submission[showPopup]) return 'border-green-500';
		else return 'border-red-500';
	}

	function countAvailability(index) {
		let cnt = 0;

		for (let p of participants) {
			if (p.submission[index]) cnt++;
		}

		return cnt;
	}

	function calculateOpacity(index) {
		if (participants.length === 0) return '';
		let percentage = (countAvailability(index) / participants.length) * 100;

		if (percentage >= 100) return 'bg-blue-300';
		if (percentage >= 75) return 'bg-blue-200';
		if (percentage >= 50) return 'bg-blue-100';
		if (percentage >= 25) return 'bg-blue-50';
		return '';
	}

	function getMaxIndex() {
		let ar = [];
		for (let i = 0; i < 7 * 15; i++) {
			ar[i] = 0;
			for (let j = 0; j < participants.length; j++) {
				if (participants[j].submission[i]) ar[i]++;
			}
		}
		console.clear();
		console.log(ar);

		let max = 0;
		for (let v of ar) max = Math.max(max, v);

		console.log('max is', max);

        for(let i=0; i<ar.length; i++) {
            if (ar[i] === max) {
                maxIndex = i;
                break;
            }
        }
	}
</script>

<div class="flex items-center space-x-4 bg-blue-100 p-5">
	<div class="font-semibold">Meeting Name: {mid}</div>

	<div class="ml-auto flex flex-col items-center space-y-1">
		<div class="flex -space-x-3">
			{#each participants as person (person.name)}
				<div
					class="overflow-hidden rounded-full border-2 border-white"
					style="width: 32px; height: 32px;"
				>
					<Avatar size={32} name={person.name} variant="beam" />
				</div>
			{/each}
		</div>
		<div class="text-sm text-gray-700">
			{participants.length} participant{participants.length === 1 ? '' : 's'}
		</div>
	</div>
</div>

<div class="mt-4 ml-2">You are participating as</div>

<div class="mt-6 ml-2 flex items-center space-x-4 text-xs">
	<div class="flex items-center space-x-1">
		<div class="h-5 w-10 border border-gray-300"></div>
		<span>0%</span>
	</div>
	<div class="flex items-center space-x-1">
		<div class="h-5 w-10 border border-gray-300 bg-blue-50"></div>
		<span>25%</span>
	</div>
	<div class="flex items-center space-x-1">
		<div class="h-5 w-10 border border-gray-300 bg-blue-100"></div>
		<span>50%</span>
	</div>
	<div class="flex items-center space-x-1">
		<div class="h-5 w-10 border border-gray-300 bg-blue-200"></div>
		<span>75%</span>
	</div>
	<div class="flex items-center space-x-1">
		<div class="h-5 w-10 border border-gray-300 bg-blue-300"></div>
		<span>100%</span>
	</div>
</div>

<div class="mt-8 mb-1 grid grid-cols-7 text-center text-sm font-semibold text-gray-700">
	{#each DAYS as day}
		<div>{day}</div>
	{/each}
</div>

<div class="mt-1 grid grid-cols-7">
	{#each arr as v, i}
		<button
			class={`flex h-8 cursor-pointer items-center justify-center border border-gray-100 text-xs ${calculateOpacity(i)}`}
			class:text-gray-300={calculateOpacity(i) === ''}
			onclick={() => (showPopup = i)}
		>
            {#if i == maxIndex}
                <span class="text-xl mr-1" title="highest availability!">⭐️</span>
            {/if}
			{toAmPm(Math.floor(i / 7) + 8)}
		</button>
	{/each}
</div>

<div
	class="top-0 right-0 bottom-0 left-0 flex items-center justify-center bg-gray-800/60"
	class:fixed={showPopup}
	class:hidden={!showPopup}
>
	<div
		class="relative m-6 flex h-[230px] w-[450px] flex-col items-center justify-center rounded-lg border bg-blue-100 p-6"
	>
		<button
			onclick={() => (showPopup = undefined)}
			class="absolute top-2 right-4 cursor-pointer text-3xl font-bold text-gray-500 hover:text-black"
			aria-label="Close"
		>
			&times;
		</button>

		<div class="text-lg">{DAYS[showPopup % 7] + ' ' + toAmPm(Math.floor(showPopup / 7) + 8)}</div>
		<div class="text-sm">{countAvailability(showPopup)}/{participants.length} available</div>
		<div class="mt-2 flex justify-center">
			<div class="mt-6 flex justify-center gap-2">
				{#each participants as person}
					<div class="flex flex-col items-center">
						<div class={`rounded-full border-4 p-1 ${getBorderClasses(person.submission)}`}>
							<div class="rounded-full bg-white p-1">
								<Avatar size={60} name={person.name} variant="beam" />
							</div>
						</div>
						<div class="mt-1 w-[70px] truncate text-center text-xs text-gray-700">
							{person.name}
						</div>
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>
