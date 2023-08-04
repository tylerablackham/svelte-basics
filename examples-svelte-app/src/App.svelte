<script>
	import Reactivity from "./reactivity.svelte"
	export let name;
</script>

<main>
	<h1>Hello {name}!</h1>
	<h2>These components help show how reactivity works</h2>
	<h3>Check out the reactivity.svelte file for some explanations</h3>
	<div style="outline-style: dashed; outline-color: gray; padding: 1em">
		<Reactivity />
	</div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>