<script>
	let search = ''
	let loading = false
	const API_URL = 'http://api.giphy.com/v1/gifs/search?api_key=HyU2YGWr4JKCaZPgMCDvpzS6g2MCyfRj&q='

	let gifs = []
	async function formSubmit(event) {
		event.preventDefault();
		loading = true
		gifs = []
		const url = `${API_URL}${search}`
		const response = await fetch(url)
		const json = await response.json()
		gifs = json.data.map(gif => gif.images.fixed_height.url)
		loading = false
	}
</script>

<style>
	.results {
		column-count: 2;
		
	}

	img {
		width: 100%;
		height: auto;
	}
</style>

<form on:submit={formSubmit}>
	<label for="search">Search</label>
	<input bind:value={search} type="text" id="search" name="search">
	<button type="submit">Search</button>
</form>

<h2>Search result for: {search}</h2>

{#if loading}
	<img alt="loading indicator" src="loading.gif">
{/if}

<div class="results">
	{#each gifs as gif}
		<img src={gif} alt="gif">
	{/each}
</div>