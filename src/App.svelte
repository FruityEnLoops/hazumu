<script>
	import "smelte/src/tailwind.css";
	import { Button, ProgressCircular } from "smelte";
	import List from "./List.svelte";
	export let name;
	let files;

	async function processFile(file) {
		let data = await file.text();
		let dataArray = JSON.parse(data);
		return dataArray.messages.filter(message => message.content != "");
	}
</script>

<main>
	<h1>{name}</h1>
	<input type="file" id="filePicker" accept="application/json" bind:files>
	<Button onclick="document.getElementById('filePicker').click();">Load JSON file</Button>
	{#if files}
		{#each Array.from(files) as file}
			{#await processFile(file) }
				<div class="center">
					<ProgressCircular/>
				</div>
			{:then data} 
				<List data={data}/>
			{/await}
		{/each}
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #da6200;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	
	#filePicker {
		display: none;
	}

	:global(html) {
		overflow-y: scroll;
	}
	
	.center {
		margin-left: 48%;
		margin-right: auto;
	}
</style>