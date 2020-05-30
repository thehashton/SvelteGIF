<script>
	let search = "";
	let loading = false;
	const API_URL = "https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=";

	let gifs = [];

	const formSubmitted = async (event) => {
		event.preventDefault();
		loading = true;
		gifs = [];
		const url = `${API_URL}${search}`;
		const response = await fetch(url);
		const json = await response.json();
		gifs = json.data.map(gif => gif.images.fixed_height.url)
		loading = false;
	}
</script>

<style>
.results {
	column-count: 3;
}

img {
	width: 100%;
}

h1, p {
	margin: 0;
}

.title p {
	margin-bottom: 20px
}

.title, form {
	text-align: center;
}
</style>

<div class="title">
	<h1>SvelteGIF</h1>
	<p>By Harry Ghazni</p>
</div>

<form on:submit={formSubmitted}>
	<input placeholder="Search for a GIF" bind:value={search} id="search" name="search">
	<button type="submit">Submit</button>
</form>

{#if loading}
	<img src={"https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif"} alt="loading">
{/if}

<div class="results">
	{#each gifs as gif}
		<img src={gif} alt="gif" />
	{/each}
</div>
