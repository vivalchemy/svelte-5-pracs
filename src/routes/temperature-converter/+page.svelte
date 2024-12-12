<script lang="ts">
	import { goto } from '$app/navigation';

	// it is better to use class to design custom getter and setter in this case and the changes need to be cyclic
	//let tempInCelsius = $state(0);
	//let tempInFahrenheit = $state(0);

	class Temperature {
		_c = $state(0);
		_f = $state(0);

		get c() {
			return this._c;
		}
		get f() {
			return this._f;
		}

		set c(value: number) {
			this._c = value;
			this._f = (value * 9) / 5 + 32;
		}

		set f(value: number) {
			this._f = value;
			this._c = ((value - 32) * 5) / 9;
		}
	}

	let temp = new Temperature();
</script>

<button
	onclick={() => goto('/')}
	class="px-4 py-2 absolute top-0 translate-y-1/2 left-0 translate-x-1/2">&lt;</button
>
<h1 class="text-5xl absolute top-0 translate-y-1/2 left-1/2 -translate-x-1/2">
	Temperature Converter
</h1>
<div class="max-w-md">
	<label for="celsius">Celsius</label>
	<input type="number" name="celsius" id="celsius" bind:value={temp.c} />
	<label for="fahrenheit">Fahrenheit</label>
	<input type="number" name="fahrenheit" id="fahrenheit" bind:value={temp.f} />
</div>
