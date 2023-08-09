<script>
	import Reactivity from "./reactivity.svelte"
	import Props from "./props.svelte"
	import Logic from "./logic.svelte"
	import Events from "./events.svelte"
	export let name;
</script>

<main>
	<h1>Hello {name}!</h1>
	<div style="display: flex; justify-content: center; justify-content: space-evenly; padding-bottom: 3em">
		<div style="outline-style: dashed; outline-color: gray; padding: 1em; max-width: fit-content">
			<h2>This component helps show how reactivity works</h2>
			<h3>Check out the reactivity.svelte file for some explanations</h3>
			<Reactivity />
		</div>
		<div style="outline-style: dashed; outline-color: gray; padding: 1em; max-width: fit-content">
			<h2>This component helps show how props works</h2>
			<h3>Check out the props.svelte file for some explanations</h3>
			<Props number={420} number2={123456789}/>
			<Props />
		</div>
		<div style="outline-style: dashed; outline-color: gray; padding: 1em; max-width: fit-content">
			<h2>This component helps show how logic works</h2>
			<h3>Check out the logic.svelte file for some explanations</h3>
			<Logic/>
		</div>
	</div>
	<div style="display: flex; justify-content: center; justify-content: space-evenly">
		<div style="outline-style: dashed; outline-color: gray; padding: 1em; max-width: fit-content">
			<h2>This component helps show how events works</h2>
			<h3>Check out the events.svelte file for some explanations</h3>
			<Events on:tickled={(e) => {alert(e.detail.response)}}
					on:tickled2={(e) => {alert(e.detail.laugh)}}/>
		</div>
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