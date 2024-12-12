<script lang="ts">
	import { goto } from '$app/navigation';

	type Options = 'one-way' | 'return';

	let selected = $state<Options>('one-way');
	let startDate = $state(getDate());
	let returnDate = $state(getDate());

	function handleSubmit(e: Event) {
		e.preventDefault();
		let msg =
			selected === 'one-way'
				? `You have booked a ${selected} flight on ${startDate}`
				: `You have booked a ${selected} flight on ${startDate} and return ticket is booked for ${returnDate}`;
		alert(msg);
	}

	function getDate() {
		const date = new Date();
		const [month, day, year] = date
			.toLocaleDateString('en-US', {
				year: 'numeric',
				month: '2-digit',
				day: '2-digit'
			})
			.split('/');
		return `${year}-${month}-${day}`;
	}

	$inspect({ selected, startDate, returnDate });
</script>

<button
	onclick={() => goto('/')}
	class="px-4 py-2 absolute top-0 translate-y-1/2 left-0 translate-x-1/2">&lt;</button
>
<h1 class="text-6xl absolute top-0 translate-y-1/2 left-1/2 -translate-x-1/2">Flight Booker</h1>

<form action="" onsubmit={handleSubmit}>
	<select name="" id="" bind:value={selected}>
		<option value="one-way">One Way</option>
		<option value="return">Return</option>
	</select>

	<label for="start-date">
		<span class="">Select the start date:</span>
	</label>
	<input
		type="date"
		name="start-date"
		id="start-date"
		bind:value={startDate}
		min={getDate()}
		required
	/>

	<label for="return-date">
		<span class={`${selected === 'one-way' && 'text-slate-700'}`}>Select the return date:</span>
	</label>
	<input
		type="date"
		name="return-date"
		id="return-date"
		disabled={selected === 'one-way'}
		required={selected !== 'one-way'}
		bind:value={returnDate}
	/>
	<button type="submit" disabled={!startDate || (selected === 'return' && returnDate < startDate)}
		>Book Flight</button
	>
</form>
