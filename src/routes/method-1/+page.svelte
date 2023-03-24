<script lang="ts">
  let error: string
	let procedimiento: any = []
  const metodo1 = (cantidad: number, semilla: number) => {
    const numerosGenerados: string[] = [];
    procedimiento = []

		console.log('Semilla ', semilla);
		if (semilla.toString().length % 2 !== 0) {
      error = 'No se permite una semilla con dígitos impares'
		}

		const digits = semilla.toString().length;
		console.log(digits);
		let initial = semilla;

		for (let i = 0; i < cantidad; i++) {
			const step1 = initial ** 2;
			const step2 = step1.toString();
			const step3 = step2.length % 2 === 1 ? '0' + step2 : step2;

			console.log(`N${i + 1}: ` + step3);
      procedimiento.push(step3)

			const step4 = step3.slice(step3.length / 4, step3.length / 4 + digits);
			numerosGenerados.push(step4);
			initial = parseInt(step4);
		}

		return numerosGenerados;
	};

	let numeros: any[] = [];

	let input = '';
	function onSubmit(e: any) {
    numeros = []
		const formData = new FormData(e.target);

		const data: any = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		numeros = metodo1(data.quantity, data.seed);
	}
</script>

<h4>Ingresar semilla</h4>
<form on:submit|preventDefault={onSubmit}>
	<input placeholder="Semilla" name="seed" />
	<input placeholder="Cantidad a generar" name="quantity" />
	<button type="submit"> Generar numeros </button>
  <h4>{error ?? ''}</h4>
</form>
<h2>Procedimiento</h2>
{#each procedimiento as pr, i}
	<li>
		{pr}
	</li>
{/each}
<h2>Probabilidades</h2>
{#each numeros as numero, i}
	<li>
		{numero} -> 0.{numero}
	</li>
{/each}
