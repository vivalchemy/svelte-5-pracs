<script lang="ts">
	import { goto } from '$app/navigation';

	let elasped = $state(0);
	let duration = $state(0);
	let interval: number;

	function handleStart() {
		interval = setInterval(() => {
			elasped += 0.1;
			if (elasped >= duration) {
				clearInterval(interval);
				elasped = duration;
			}
		}, 100);
	}

	function handleReset() {
		elasped = 0;
		handleStart();
	}

	$effect(() => {
		if (!duration) return;
		elasped = 0;
		handleStart();
		return () => clearInterval(interval);
	});

	$inspect({ duration, elasped });
</script>

<button
	onclick={() => goto('/')}
	class="px-4 py-2 absolute top-0 translate-y-1/2 left-0 translate-x-1/2">&lt;</button
>
<h1 class="text-5xl absolute top-0 translate-y-1/2 left-1/2 -translate-x-1/2">Timer</h1>
<div class="max-w-md">
	<progress value={elasped} max={duration}></progress>
	<span>{elasped.toFixed(2)}s</span>
	<input type="range" min="1" max="10" bind:value={duration} />
	<button onclick={handleReset}>Reset</button>
</div>
