<script lang="ts">
	type Person = {
		name: string;
		surname: string;
	};

	let people = $state<Person[]>([
		{
			name: 'John',
			surname: 'Doe'
		},
		{
			name: 'Jane',
			surname: 'Doe'
		},
		{
			name: 'John',
			surname: 'Smith'
		}
	]);

	let selected = $state<Person>();
	let person = $state<Person>({
		name: '',
		surname: ''
	});

	let filterTerm = $state<string>('');

	let filteredPeople = $derived<Person[]>(
		people.filter(
			(person) =>
				!filterTerm ||
				person.name.toLowerCase().startsWith(filterTerm.toLowerCase()) ||
				person.surname.toLowerCase().startsWith(filterTerm.toLowerCase())
		)
	);

	function handleCreate() {
		people.push(person);
		person = { name: '', surname: '' };
	}

	function handleUpdate() {
		let index = people.indexOf(selected as Person);
		people[index] = person;
	}

	function handleDelete() {
		people = people.filter((person) => person !== selected);
	}

	$inspect(filteredPeople);
</script>

<div class="flex gap-4">
	<div>
		<div class="search">
			<label class="flex gap-2">
				<span>Filter prefix:</span>
				<input type="text" bind:value={filterTerm} />
			</label>
		</div>

		<label class="people">
			<span class="sr-only">Names:</span>
			<select bind:value={selected} size="5">
				{#each filteredPeople as person}
					<option value={person}>
						{person.name}
						{person.surname}
					</option>
				{/each}
			</select>
		</label>
	</div>
	<div>
		<div class="">
			<label class="flex gap-2">
				<span>Name:</span>
				<input type="text" bind:value={person.name} />
			</label>
			<label class="flex gap-2">
				<span>Surname:</span>
				<input type="text" bind:value={person.surname} />
			</label>
		</div>
	</div>
</div>
<div class="flex gap-4">
	<button onclick={handleCreate}>Create</button>
	<button onclick={handleUpdate}>Update</button>
	<button onclick={handleDelete}>Delete</button>
</div>
