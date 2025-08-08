<script>
	import 'bootstrap/dist/js/bootstrap.js'
    import 'bootstrap/dist/css/bootstrap.css';
    import 'bootstrap-icons/font/bootstrap-icons.css'
	import NavBar from '$lib/components/NavBar.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<title>Num Bases</title>
</svelte:head>

<main>
	<NavBar/>
	<div class="container-fluid">
		{@render children?.()}
	</div>
</main>

<style>
	@font-face {
		font-family: 'fonte';
		src: url('../lib/assets/font.otf');
	}
	* {
		font-family: 'fonte';
	}
</style>