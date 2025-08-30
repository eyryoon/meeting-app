<script>
	import QRCode from "@trasherdk/svelte-qrcode";

	const code = 'abc';
	const link = 'http://localhost:5174/meeting/' + code;
</script>

<div class="flex min-h-screen flex-col items-center justify-center">
	<div>
    <QRCode content={link}></QRCode>
  </div>
	<div>
		<a href={link}>
			{link}
		</a>
	</div>
</div>
