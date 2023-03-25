<script lang="ts">
	let error: string;
	const metodo6 = (cantidad: number, semillas: any[], m: number) => {
		const numerosGenerados: string[] = [];

		let first = semillas[0];
		let last = semillas[semillas.length - 1];
		let lastCounter = semillas.length - 1;

		for (let i = 0; i < cantidad; i++) {
			const newNumber = (first + last) % m;
			semillas.push(newNumber);
			lastCounter++;
			first = semillas[i + 1];
			last = semillas[lastCounter];
			numerosGenerados.push((newNumber / (m - 1)).toFixed(4).toString());
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
		numeros = metodo6(
			parseInt(data.quantity),
			[
				parseInt(data.x1),
				parseInt(data.x2),
				parseInt(data.x3),
				parseInt(data.x4),
				parseInt(data.x5)
			],
			parseInt(data.m)
		);
	}
</script>

<div class="container shadow">
	<h1>Congruencial aditivo</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="x1" name="x1" />
		<input placeholder="x2" name="x2" />
		<input placeholder="x3" name="x3" />
		<input placeholder="x4" name="x4" />
		<input placeholder="x5" name="x5" />
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
