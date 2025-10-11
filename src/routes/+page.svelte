<script>
	let meetingName = '';


	function createMeeting() {
		let meetings = localStorage.getItem("meetings");

		if(meetings === null) {
			meetings = [];
		} else {
			meetings = JSON.parse(meetings);
		}

		let meeting = {
			name: meetingName,
			submissions: []
		}


		localStorage.setItem("meetings", JSON.stringify([...meetings, meeting]));
	}
</script>

<div class="bg1 flex min-h-screen flex-col items-center justify-center bg-cover bg-center space-y-8">
	<h1 class="text-6xl font-extrabold text-blue-600">
		AppName
	</h1>

	<div class="bg-white border border-gray-200 flex flex-col items-center p-10 rounded shadow-lg max-w-sm w-full">
		<input
			type="text"
			placeholder="Name of your meeting"
			bind:value={meetingName}
			class="bg-white w-64 rounded border border-gray-300 px-4 py-2 text-sm"
		/>

		<a href="/new" on:click|preventDefault={() => {
			if (meetingName.trim()) {
				createMeeting();
				window.location.href = "/new";
			}
		}}>
			<button
				class="btn mt-6 bg-red-300 text-white px-4 py-2 rounded-md shadow hover:bg-red-400 transition font-semibold"
			>
				Create Meeting
			</button>
		</a>
	</div>
</div>
