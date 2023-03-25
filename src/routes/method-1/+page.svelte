<script lang="ts">
	let error: string | undefined;
	let procedimiento: any = [];
	const metodo1 = (cantidad: number, semilla: number) => {
		error = undefined;
		const numerosGenerados: string[] = [];
		procedimiento = [];

		console.log('Semilla ', semilla);
		if (semilla % 2 === 0) {
			error = 'No se permite una semilla impar';
			return [0];
		}

		const digits = semilla.toString().length;
		console.log(digits);
		let initial = semilla;

		for (let i = 0; i < cantidad; i++) {
			const step1 = initial ** 2;
			const step2 = step1.toString();
			const step3 = step2.length % 2 === 1 ? '0' + step2 : step2;

			procedimiento.push(step3);

			const step4 = step3.slice(step3.length / 4, step3.length / 4 + digits);
			numerosGenerados.push(step4);
			initial = parseInt(step4);
		}

		return numerosGenerados;
	};

	let numeros: any[] = [];

	let input = '';
	function onSubmit(e: any) {
		numeros = [];
		const formData = new FormData(e.target);

		const data: any = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		numeros = metodo1(data.quantity, data.seed);
	}
</script>

<div class="container shadow">
	<h1>Algoritmo de cuadrados medios</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="Cantidad a generar" name="quantity" />
		<button type="submit"> Generar numeros </button>
		<h4>{error ?? ''}</h4>
	</form>
	{#if numeros.length > 0 && !error}
		<h2>Procedimiento</h2>
	{/if}
	{#each procedimiento as pr, i}
		<li>
			{pr}
		</li>
	{/each}
	{#if numeros.length > 0 && !error}
		<h2>Probabilidades</h2>
	{/if}
	{#each numeros as numero, i}
		<li>
			{numero} >>> 0.{numero}
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
