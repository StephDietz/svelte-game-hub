<script>
	import { Router, Link, Route } from "svelte-routing";
	import Welcome from './Pages/Welcome.svelte';
	import GameHub from './Pages/GameHub.svelte';

	export let url = "";

	let name = 'Test';
</script>

<main>
	<div class="w-full bg-white shadow-lg sticky flex items-center lg:px-40 md:px-20 py-4 px-8">
		<div class="flex">
			<div class="bg-indigo-500 w-8 h-8 opacity-75 rounded-full"></div>
			<div class="bg-indigo-500 w-8 h-8 rounded-full opacity-50 -ml-5"></div>
		</div>
		<div class="font-bold uppercase text-indigo-500 ml-2">Game Hub</div>
	</div>
	<Router url="{url}">
	<!-- <nav>
		<Link to="/">Welcome</Link>
		<Link to="game-hub">Game Hub</Link>
	</nav> -->
	<div>
		<Route path="game-hub" component="{GameHub}" />
		<Route path="/"><Welcome /></Route>
	</div>
	</Router>
</main>
