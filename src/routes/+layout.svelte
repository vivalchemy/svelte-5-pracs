<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="h-screen w-screen flex flex-col items-center justify-center">
	{@render children()}
</div>
