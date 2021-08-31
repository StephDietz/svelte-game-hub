<script>
  import { Router, Link, Route } from "svelte-routing";
  import GameHub from './GameHub.svelte';

  export let url = "";
</script>

<main>
  <div class="flex flex-col items-center p-8 md:p-20 lg:p-40">
    <div class="font-bold text-6xl mb-12">Welcome!</div>
    <Link class="bg-indigo-500 text-white font-bold rounded p-4" to="game-hub">Game Hub</Link>
  </div>

	<Router url="{url}">
	<div>
		<Route path="game-hub" component="{GameHub}" />
	</div>
	</Router>
</main>
