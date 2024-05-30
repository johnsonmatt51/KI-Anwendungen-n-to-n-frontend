<script>
    import { PUBLIC_BASE_URL } from '$env/static/public';
 	import axios from "axios";

	let circles = [
		{id: 1, name: `Kreis 1` },
		{id: 2, name: `Kreis 2` },
		{id: 3, name: `Kreis 3` },
		{id: 4, name: `Kreis 4` },
		{id: 5, name: `Kreis 5` },
		{id: 6, name: `Kreis 6` },
		{id: 7, name: `Kreis 7` },
		{id: 8, name: `Kreis 8` },
		{id: 9, name: `Kreis 9` },
		{id: 10, name: `Kreis 10` },
		{id: 11, name: `Kreis 11` },
	];

	let price;
	let rating = '...'
	let price_slider = 3
	let selected;
	function handleSubmit() {
		let url =
            PUBLIC_BASE_URL +
            "/api/prediction/restaurant?circle=" +
            selected.id +
            "&price_numeric=" +
            price_slider;
        console.log(url);
        axios.get(url).then((response) => {
            rating = response.data + " / 5";
        });
	}
</script>
<div class="container text-center">

	<h1>In the chosen circle for your chosen price range, you can expect the following rated restaurants: {rating}</h1>

	<div class="row justify-content-md-center">
	  <div class="col col-lg-2">
	  	<label>price</label>
	  	<input type="range" min=1 max=5 bind:value={price_slider} class="slider" id="myRange">
	  </div>
	  <div class="col col-lg-2">
		<select class="form-select" bind:value={selected}>
			{#each circles as circle}
				<option value={circle}>
					{circle.name}
				</option>
			{/each}
		</select>
	  </div>
	  <div class="col-md-auto">
		<button type="button" class="btn btn-primary" on:click={handleSubmit}>rating estimation</button>
	  </div>
	</div>
  </div>
