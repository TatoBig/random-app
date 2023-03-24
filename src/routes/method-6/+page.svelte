<script lang="ts">
	let error: string;
	let procedimiento: any = [];
	const metodo6 = (cantidad: number, semillas: any[], m: number) => {
		console.log('Semillas ', semillas);
		console.log('m ', m);

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

	let input = '';
	function onSubmit(e: any) {
		numeros = [];
		const formData = new FormData(e.target);

		const data: any = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		numeros = metodo6(data.quantity, [data.x1, data.x2, data.x3, data.x4], data.m);
	}
</script>

<h4>Ingresar semilla</h4>
<form on:submit|preventDefault={onSubmit}>
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
<h2>Probabilidades</h2>
{#each numeros as numero, i}
	<li>
		{numero}
	</li>
{/each}
