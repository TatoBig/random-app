<script lang="ts">
	let error: string | undefined;
	const metodo5 = (cantidad: number, semilla: number, k: number, g: number) => {
		const numerosGenerados: string[] = [];
		error = undefined;
		if (semilla % 2 === 0) {
			error = 'No es posible usar una semilla impar';
			return [0];
		}
		if (cantidad <= 0 || semilla <= 0 || k <= 0 || g <= 0) {
			error = 'Solo es posible usar números positivos';
			return [0];
		}

		let x = semilla;
		const a = 5 + 8 * k;
		const m = 2 ** g;

		for (let i = 0; i < cantidad; i++) {
			x = (a * x) % m;
			numerosGenerados.push((x / (m - 1)).toFixed(4).toString());
		}

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
		numeros = metodo5(
			parseInt(data.quantity),
			parseInt(data.seed),
			parseInt(data.k),
			parseInt(data.g)
		);
	}
</script>

<div class="container shadow">
	<h1>Congruencial multiplicativo</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="k" name="k" />
		<input placeholder="g" name="g" />
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
