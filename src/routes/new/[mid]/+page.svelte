<script>
	import QRCode from '@trasherdk/svelte-qrcode';
	const p = $props();
	const mid = p.params.mid;

	const link = 'http://localhost:5173/meeting/' + mid;

	function copyLink() {
		navigator.clipboard.writeText(link);
		// Could add a toast notification here if wanted
	}
</script>

<div class="rounded-lg p-8">
	<section class="py-12 text-center">
		<h1 class="text-5xl leading-tight font-extrabold text-sky-600">meeting is ready!</h1>
		<p class="mx-auto mt-4 max-w-2xl text-gray-600">
			share this QR code or link with your friends to join
		</p>
	</section>

	<section class="mx-auto max-w-lg rounded-xl border border-gray-100 bg-white p-8 shadow-lg">
		<div class="text-center">
			<div class="mb-6 flex justify-center">
				<QRCode content={link} />
			</div>

			<div class="mb-4">
				<p class="mb-2 text-sm font-medium text-gray-700">Meeting Link:</p>
				<div class="rounded-lg border bg-gray-50 p-3">
					<a href={link} class="text-lg break-all text-sky-500 hover:text-sky-700 hover:underline">
						http://localhost:5173/meeting/<span class="font-bold text-sky-600">{mid}</span>
					</a>
				</div>
			</div>

			<div class="flex justify-center gap-3">
				<button
					class="inline-flex items-center gap-2 rounded-md bg-sky-500 px-4 py-2 font-semibold text-white transition hover:bg-sky-600"
					on:click={copyLink}
				>
					Copy Link
				</button>
				<a
					href="/"
					class="inline-flex items-center gap-2 rounded-md border border-gray-300 bg-white px-4 py-2 font-semibold text-gray-700 transition hover:bg-gray-50"
				>
					Create Another
				</a>
			</div>
		</div>
	</section>
</div>
