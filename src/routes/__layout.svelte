<script>
	import '../app.postcss';
	import Nav from '../components/nav.svelte';
</script>


<!--Div que permite centrar el contenido y añadir un padding a todos sus aldos-->
<div class="p-8 max-w-6xl mx-auto">
    <Nav />
	<slot></slot>
</div>

<style>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>
