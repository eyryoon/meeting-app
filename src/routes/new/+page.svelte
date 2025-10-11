<script>
	import QRCode from '@trasherdk/svelte-qrcode';

	function generateRandomId(length = 10) {
		return Math.random()
			.toString(36)
			.substring(2, 2 + length);
	}

	const code = generateRandomId(6);
	const link = 'http://localhost:5173/meeting/' + code;
</script>

<div class="flex min-h-screen flex-col">
	<div class="fixed w-full bg-blue-100 p-12 text-center text-3xl">share with friends!!!</div>
	<div class="flex flex-1 flex-col items-center justify-center">
		<div class>
			<QRCode content={link}></QRCode>
		</div>
		<div class="text-2xl text-blue-400 mt-6 hover:text-blue-800 hover:underline">
			<a href={link}>
				http://localhost:5173/meeting/<span class="text-4xl text-blue-500">{code}</span>
			</a>
		</div>
	</div>
</div>
