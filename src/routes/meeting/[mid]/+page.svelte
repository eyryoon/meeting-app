<script>
	const p = $props();
	const mid = p.params.mid;
</script>

<div>GROUP: {mid}</div>

<div>Select which times you are available</div>

<div class="grid grid-cols-8">
	<div></div>
	<div>sun</div>
	<div>mon</div>
	<div>tue</div>
	<div>wed</div>
	<div>thu</div>
	<div>fri</div>
	<div>sat</div>

	<div>12pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>1pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>2pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>3pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>4pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>5pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>6pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>7pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>8pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>9pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>10pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}

	<div>11pm</div>
	{#each ['', '', '', '', '', '', ''] as v}
		<div class={v}>-</div>
	{/each}
</div>
