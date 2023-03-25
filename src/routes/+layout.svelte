<script>
	import { page } from '$app/stores';
	console.log($page.url.pathname);
</script>

<div class="layout">
	{#if $page.url.pathname !== '/'}
		<a href="/">Regresar al menu</a>
	{/if}
	<slot />
</div>

<style>
	.layout {
		display: flex;
		width: 100%;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		margin-top: 5%;
		font-family: Arial, Helvetica, sans-serif;
	}
</style>
