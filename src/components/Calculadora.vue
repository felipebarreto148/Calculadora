<template>
	<div class="calculadora">
		<div class="display">{{ total || 0 }}</div>
		<div @click="limpar" id="clear" class="botao">C</div>
		<div class="botao operadores">()</div>
		<div @click="porcentagem" class="botao operadores">%</div>
		<div @click="dividir" class="botao operadores">/</div>
		<div @click="juntarNumeros('7')" class="botao">7</div>
		<div @click="juntarNumeros('8')" class="botao">8</div>
		<div @click="juntarNumeros('9')" class="botao">9</div>
		<div @click="multiplicar" class="botao operadores">x</div>
		<div @click="juntarNumeros('4')" class="botao">4</div>
		<div @click="juntarNumeros('5')" class="botao">5</div>
		<div @click="juntarNumeros('6')" class="botao">6</div>
		<div @click="subtrair" class="botao operadores">-</div>
		<div @click="juntarNumeros('1')" class="botao">1</div>
		<div @click="juntarNumeros('2')" class="botao">2</div>
		<div @click="juntarNumeros('3')" class="botao">3</div>
		<div @click="somar" class="botao operadores">+</div>
		<div @click="alterarSinal" class="botao">+/-</div>
		<div @click="juntarNumeros('0')" class="botao">0</div>
		<div @click="adicionarPonto" class="botao">.</div>
		<div @click="resultado" id="result" class="botao operadores">=</div>
	</div>
</template>

<script>
	export default {
		name: 'Calculadora',
		data() {
			return {
				total: '',
				numeroAnterior: null,
				operador: null,
				operadorClicado: false,
			};
		},
		methods: {
			limpar() {
				//Responsável por limpar a calculadora
				this.total = '';
			},
			alterarSinal() {
				//Responsável por colocar o sinal '-' ou '+'
				this.total =
					this.total.charAt(0) === '-' ? this.total.slice(1) : `-${this.total}`;
			},
			porcentagem() {
				//Responsável por realizar operações de 'porcentagem'
				this.total = parseFloat(this.total) / 100;
			},
			juntarNumeros(numero) {
				//Responsável por juntar os números clicados no display da calculadora
				if (this.operadorClicado) {
					this.total = '';
					this.operadorClicado = false;
				}
				this.total = `${this.total}${numero}`;
			},
			adicionarPonto() {
				//Responsável por adicionar o ponto
				if (this.total.indexOf('.') == -1) {
					this.juntarNumeros('.');
				}
			},
			setarValor() {
				this.numeroAnterior = this.total;
				this.operadorClicado = true;
			},
			dividir() {
				//Responsável por realizar operações de 'Divisão'
				this.operador = (num1, num2) => num1 / num2;
				this.setarValor();
			},
			multiplicar() {
				//Responsável por realizar operações de 'Multiplicação'
				this.operador = (num1, num2) => num1 * num2;
				this.setarValor();
			},
			somar() {
				//Responsável por realizar operações de 'Soma'
				this.operador = (num1, num2) => num1 + num2;
				this.setarValor();
			},
			subtrair() {
				//Responsável por realizar operações de 'Subtração'
				this.operador = (num1, num2) => num1 - num2;
				this.setarValor();
			},
			resultado() {
				//Responsável por mostrar o resultado no display
				this.total = `${this.operador(
					parseFloat(this.numeroAnterior),
					parseFloat(this.total),
				)}`;
				this.numeroAnterior = null;
			},
		},
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.calculadora {
		margin: 0 auto;
		width: 350px;
		font-size: 40px;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-auto-rows: minmax(50px, auto);
	}

	.display {
		grid-column: 1 / 5;
		background-color: #333;
		color: white;
		border-radius: 20px;
		margin-bottom: 20px;
	}

	.botao {
		background-color: #f2f2f2;
		border: none /* 1px solid #999 */;
		border-radius: 30px;
		margin: 5px;
		cursor: pointer;
		text-decoration: none;
	}

	.operadores {
		background-color: black;
		color: limegreen;
	}

	#result,
	#clear {
		background: green;
		color: black;
	}

	.botao:hover {
		transform: scale(1.1);
		box-shadow: 5px 5px 5px rgba(68, 68, 68, 0.8);
	}
</style>
