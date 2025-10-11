<script>
	const p = $props();
	const mid = p.params.mid;

	const DAYS = "Sun,Mon,Tue,Wed,Thu,Fri,Sat".split(",")
	let arr = $state(new Array(105).fill(false));
  let participantName = "";

	function toAmPm(hr) {
    if (hr <= 11) return hr + "AM";
	else if (hr == 12) return hr + "PM"
    else return (hr-12) + "PM";
  }

  function addSubmission() {
    let meetings = JSON.parse(localStorage.getItem("meetings"));

    let submission = {
      name: participantName,
      submission: arr
    };
    meetings = meetings.map((m) => m.name === mid ? {...m, submissions: [...m.submissions, submission]} : m);
    localStorage.setItem("meetings", JSON.stringify(meetings));
  }
</script>

<div class="p-5 bg-blue-100 font-semibold">GROUP: {mid}</div>

<div class="mt-4 ml-2 flex items-center space-x-2">
  <span>Enter your name</span>
  <input
    type="text"
    placeholder="Type here"
    bind:value={participantName}
    class="border border-gray-300 px-2 py-1 rounded text-sm"
  />
</div>

<div class="mt-6 mb-2 ml-2">Select which times you are available:</div>


<div class="grid grid-cols-7">
  {#each arr as v, i}
    <button 
      class="border border-gray-100 h-8 text-xs flex justify-center items-center hover:bg-blue-50 cursor-pointer"
      class:bg-blue-200={v}
      class:text-gray-300={!v}
      onclick={() => arr[i] = !arr[i]}
    >
      {DAYS[i%7]} {toAmPm(Math.floor(i/7)+8)}
    </button>
  {/each}
</div>


<div class="flex justify-end mt-6 mr-2">
	<a href={`/meeting/${mid}/results`}><button onclick={addSubmission} class="btn bg-red-300 text-white px-4 py-2 rounded-md shadow hover:bg-red-400 transition font-semibold">Submit</button></a>
</div>
