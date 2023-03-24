<script lang="ts">
	let error: string;
	let procedimiento: any = [];
	const metodo5 = (cantidad: number, semilla: number, k: number, g: number) => {
		const numerosGenerados: string[] = [];

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

	let input = '';
	function onSubmit(e: any) {
		numeros = [];
		const formData = new FormData(e.target);

		const data: any = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		numeros = metodo5(data.quantity, data.seed, data.k, data.g);
	}
</script>

<h4>Ingresar semilla</h4>
<form on:submit|preventDefault={onSubmit}>
	<input placeholder="Semilla" name="seed" />
	<input placeholder="k" name="k" />
	<input placeholder="g" name="g" />
	<input placeholder="Cantidad a generar" name="quantity" />
	<button type="submit"> Generar numeros </button>
	<h4>{error ?? ''}</h4>
</form>
<h2>Probabilidades</h2>
{#each numeros as numero, i}
	<li>
		{numero}
	</li>
{/each}
