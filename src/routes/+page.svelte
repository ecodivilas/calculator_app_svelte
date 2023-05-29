<script>
	let total = 0;
	let console = '';
	let state = null;

	function resolveState() {
		switch (state) {
			case 'add':
				total += parseFloat(console);
				console = '0';
				break;
			case 'substract':
				total -= parseFloat(console);
				console = '0';
				break;
			case 'multiply':
				total *= parseFloat(console);
				console = '0';
				break;
			case 'divide':
				total /= parseFloat(console);
				console = '0';
				break;
			default:
				total = parseFloat(console);
				console = '0';
				break;
		}
	}

	function setOperation(operation) {
		resolveState();
		state = operation;
	}

	function setValue(value) {
		if (console.toString() == '0' || state == 'equal') {
			console = '';
		}
		if (state == 'equal') {
			state = null;
		}
		if (value == 'C') {
			total = 0;
			state = null;
			console = '';
			return;
		}
		console = console + value;
	}

	function equal() {
		resolveState();
		console = total;
		state = 'equal';
	}
</script>

<h1>Calculator in SvelteKit</h1>

<br />

<div class="container">
	<div class="calculator">
		<input type="text" bind:value={console} readonly="true" />
		<div class="buttons">
			<div class="operations">
				<button on:click={() => setOperation('add')}>+</button>
				<button on:click={() => setOperation('substract')}>-</button>
				<button on:click={() => setOperation('multiply')}>&times;</button>
				<button on:click={() => setOperation('divide')}>&divide;</button>
			</div>
			<div class="numbers">
				<div class="top">
					<button on:click={() => setValue('7')}>7</button>
					<button on:click={() => setValue('8')}>8</button>
					<button on:click={() => setValue('9')}>9</button>
				</div>
				<div class="middle">
					<button on:click={() => setValue('4')}>4</button>
					<button on:click={() => setValue('5')}>5</button>
					<button on:click={() => setValue('6')}>6</button>
				</div>
				<div class="bottom">
					<button on:click={() => setValue('1')}>1</button>
					<button on:click={() => setValue('2')}>2</button>
					<button on:click={() => setValue('3')}>3</button>
				</div>
				<div class="extra">
					<button on:click={() => setValue('0')}>0</button>
					<button on:click={() => setValue('.')}>.</button>
					<button on:click={() => setValue('C')}>C</button>
				</div>
			</div>
			<div class="equal">
				<button on:click={equal}>=</button>
			</div>
		</div>
	</div>
</div>

<style>
	h1 {
		margin-top: 50px;
		text-align: center;
		font-size: 30px;
	}
	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100vw;
	}
	.calculator {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 5px;
		width: 300px;
		height: 288px;
		border: 1px solid #eee;
		box-shadow: 2px 2px 2px #eee;
		padding: 10px;
		background-color: #232b2b;
		border-radius: 10px;
	}
	.buttons {
		height: 240px;
		width: 100%;
	}
	.calculator input {
		width: 85.6%;
		padding: 20px;
		outline: none;
		text-align: right;
		font-size: 20px;
	}
	.calculator .buttons {
		display: flex;
		flex-wrap: wrap;
	}
	.calculator .buttons .operations {
		display: flex;
		justify-content: space-between;
		width: 100%;
		height: 39.5px;
		margin-bottom: 5px;
	}
	.calculator .buttons .operations button {
		width: 23.6%;
	}
	.calculator .buttons .numbers {
		width: 74.5%;
		height: 80%;
	}
	.calculator .buttons .numbers > div {
		display: flex;
		justify-content: space-between;
	}
	.calculator .buttons .numbers > div button {
		width: 31.5%;
		height: 39.5px;
		margin-bottom: 5px;
	}
	.calculator .equal {
		width: 25%;
	}
	.calculator .equal button {
		margin-left: 7%;
		width: 95%;
		height: 98%;
		background: #fd4e02;
		color: #eee;
		border-radius: 4px;
	}
	.calculator button {
		outline: none;
	}
</style>
