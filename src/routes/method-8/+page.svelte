<script lang="ts">
	let error: string | undefined;
	const metodo8 = (cantidad: number, semilla: number, m: number) => {
		const numerosGenerados: string[] = [];
		error = undefined;

		let x = semilla;

		for (let i = 0; i < cantidad; i++) {
			x = x ** 2 % m;
			numerosGenerados.push((x / (m - 1)).toFixed(4).toString());
		}

		console.log(numerosGenerados);

		return numerosGenerados;
	};

	let numeros: any[] = [];

	function onSubmit(e: any) {
		numeros = [];
		const formData = new FormData(e.target);

		const data: any = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		numeros = metodo8(parseInt(data.quantity), parseInt(data.seed), parseInt(data.m));
	}
</script>

<div class="container shadow">
	<h1>Algoritmo de Blum, Blum y Shub</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="m" name="m" />
		<input placeholder="Cantidad a generar" name="quantity" />
		<button type="submit"> Generar numeros </button>
		<h4>{error ?? ''}</h4>
	</form>
	{#if numeros.length > 0 && !error}
		<h2>Probabilidades</h2>
	{/if}
	{#each numeros as numero, i}
		<li>
			{numero}
		</li>
	{/each}
</div>

<style>
	.container {
		display: flex;
		background-color: whitesmoke;
		padding: 16px;
		flex-direction: column;
		align-items: center;
		width: 50%;
	}

	.shadow {
		filter: drop-shadow(0 10px 8px rgb(0 0 0 / 0.04)) drop-shadow(0 4px 3px rgb(0 0 0 / 0.1));
	}

	input {
		margin-bottom: 12px;
	}
</style>
