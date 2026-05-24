<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
	import 'bootstrap/dist/css/bootstrap.min.css';
	import 'animate.css';
	import '@fortawesome/fontawesome-free/css/all.min.css';
	import '../app.css'
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}
