<script>
	import { onMount } from 'svelte';
	import {Router, Link, Route} from 'svelte-routing';
	import Masat from './pages/Masat.svelte';
	import Home from './pages/Home.svelte';
	import Navbar from './partials/Navbar.svelte';
	import Select from './components/Select.svelte'



	
	
</script>

<main>
	<Router>
		<Route path="masat" component={Masat} />
		<Route path="/" component={Home} />
	</Router>
</main>

<style>

	
</style>
