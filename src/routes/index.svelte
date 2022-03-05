<script>
	import Navbar from '$lib/Navbar.svelte';
	import Articles from '$lib/ArticleList.svelte';
</script>

<Navbar />
<Articles />

<style>
:global(body, html) {
	width: 100vw;
	height: 100vh;
	background-color: #DBEAFE;
	margin: 0;
	font-family: 'Jost', sans-serif;
	font-display: swap;
}

:global(body) {
	scrollbar-color: #2563EB #DBEAFE;
	overflow-y: scroll;
}

:global(::-webkit-scrollbar-thumb) {
	color: #2563EB;
}
</style>
