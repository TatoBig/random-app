<script lang="ts">
	let error: string | undefined;
	let procedimiento: any = [];
	const metodo2 = (cantidad: number, semilla: number, semilla2: number) => {
		procedimiento = [];
		error = undefined;
		const numerosGenerados: string[] = [];
		if (semilla.toString().length !== semilla2.toString().length) {
			error = 'Las semillas no tienen la misma cantidad de dígitos';
			return [0];
		}

		if (semilla % 2 === 0 || semilla2 % 2 === 0) {
			error = 'No se permite una semilla impar';
			return [0];
		}

		const digits = semilla.toString().length;
		console.log(digits);
		let initial = semilla;
		let second = semilla2;

		for (let i = 0; i < cantidad; i++) {
			const step1 = initial * second;
			const step2 = step1.toString();
			const step3 = digits % 2 === 1 && step2.length % 2 !== 1 ? '0' + step2 : step2;
			procedimiento.push(step3);

			const step4 = step3.slice(step3.length / 4 + 1, step3.length / 4 + digits + 1);
			numerosGenerados.push(step4);
			initial = second;
			second = parseInt(step4);
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
		numeros = metodo2(data.quantity, data.seed, data.seed2);
	}
</script>

<div class="container shadow">
	<h1>Algoritmo productos medios</h1>
	<form on:submit|preventDefault={onSubmit} class="container">
		<input placeholder="Semilla" name="seed" />
		<input placeholder="Semilla 2" name="seed2" />
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
