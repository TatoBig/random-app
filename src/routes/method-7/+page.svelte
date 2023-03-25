<script lang="ts">
	let error: string | undefined;
	const metodo7 = (
		cantidad: number,
		semilla: number,
		a: number,
		b: number,
		c: number,
		m: number
	) => {
		const numerosGenerados: string[] = [];
		error = undefined;
		if (a % 2 !== 0) {
			error = '"a" debe ser un número par';
		}
		if (c % 2 === 0) {
			error = '"c" debe ser un número impar';
		}

		let x = semilla;

		for (let i = 0; i < cantidad; i++) {
			x = (a * x ** 2 + b * x + c) % m;
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
		numeros = metodo7(
			parseInt(data.quantity),
			parseInt(data.seed),
			parseInt(data.a),
			parseInt(data.b),
			parseInt(data.c),
			parseInt(data.m)
		);
	}
</script>

<div class="container shadow">
	<h1>Algoritmo Congruencial Cuadrático</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="a" name="a" />
		<input placeholder="b" name="b" />
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
