<script lang="ts">
	let error: string;
	let procedimiento: any = [];
	const metodo4 = (cantidad: number, semilla: number, a: number, c: number, m: number) => {
		if (semilla % 2 === 0) {
			error = 'No es posible usar una semilla par'
			return [0]
		}
		const numerosGenerados: string[] = [];

		let x = semilla;

		for (let i = 0; i < cantidad; i++) {
			x = (a * x + c) % m;
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
		numeros = metodo4(data.quantity, data.seed, data.a, data.c, data.m);
	}
</script>

<h4>Ingresar semilla</h4>
<form on:submit|preventDefault={onSubmit}>
	<input placeholder="Semilla" name="seed" />
	<input placeholder="a" name="a" />
	<input placeholder="c" name="c" />
	<input placeholder="m" name="m" />
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
