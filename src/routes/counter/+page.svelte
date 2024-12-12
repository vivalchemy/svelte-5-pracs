<script lang="ts">
	import { goto } from '$app/navigation';

	let counter = $state(0);
</script>

<button
	onclick={() => goto('/')}
	class="px-4 py-2 absolute top-0 translate-y-1/2 left-0 translate-x-1/2">&lt;</button
>
<h1 class="text-6xl absolute top-0 translate-y-1/2 left-1/2 -translate-x-1/2">Counter</h1>
<h1 class="text-6xl">{counter}</h1>

<div class="flex gap-4 mt-4">
	<button onclick={() => counter++} class=" px-4 py-2 rounded-lg">+</button>
	<button onclick={() => counter--} class=" px-4 py-2 rounded-lg">-</button>
	<button onclick={() => (counter = 0)} class=" px-4 py-2 rounded-lg">Reset</button>
</div>
