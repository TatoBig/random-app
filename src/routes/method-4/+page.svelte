<script lang="ts">
	let error: string | undefined;
	const metodo4 = (cantidad: number, semilla: number, a: number, c: number, m: number) => {
		if (cantidad <= 0 || semilla <= 0 || a <= 0 || c <= 0 || m <= 0) {
			error = 'Solo es posible usar números positivos';
			return [0];
		}
		const numerosGenerados: string[] = [];

		let x = semilla;

		for (let i = 0; i < cantidad; i++) {
			x = (a * x + c) % m;
			console.log(x);
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
		numeros = metodo4(
			parseInt(data.quantity),
			parseInt(data.seed),
			parseInt(data.a),
			parseInt(data.c),
			parseInt(data.m)
		);
	}
</script>

<div class="container shadow">
	<h1>Congruencial mixto (algoritmo lineal)</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="a" name="a" />
		<input placeholder="c" name="c" />
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
