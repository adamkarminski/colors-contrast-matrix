<template>
	<div class="container">
		<nav class="nav">
			<h1>Colors matrix</h1>
		</nav>
		<div class="main">
			<div class="main__data">
				<label class="main__data__font__label" for="main__data__font">Fonts</label>
				<textarea v-model="fonts" name="main__data__font" id="" cols="30" rows="10"> </textarea>

				<label class="main__data__background__label" for="main__data__background">Backgrounds</label>
				<textarea v-model="backgrounds" name="main__data__background" id="" cols="30" rows="10"> </textarea>

				<button @click="renderColors">Rerender matrix</button>
			</div>
			<div class="main__render">
				<ColorsMatrix :colors="colors" />
			</div>
		</div>
	</div>
</template>

<script>
	import ColorsMatrix from './components/ColorsMatrix.vue';

	export default {
		components: { ColorsMatrix },
		data() {
			return {
				fonts: `gray900: #1F2534\ngray800: #434A5A\ngray700: #6F7285\ngray600: #868C9E\ngray500: #A7ACBD\ngray400: #BDC1CD\ngray300: #CDD0DA\ngray200: #E6E8EE\ngray100: #EFF0F3\ngray50: #F6F6F8`,
				backgrounds: `gray900: #1F2534\ngray800: #434A5A\ngray700: #6F7285\ngray600: #868C9E\ngray500: #A7ACBD\ngray400: #BDC1CD\ngray300: #CDD0DA\ngray200: #E6E8EE\ngray100: #EFF0F3\ngray50: #F6F6F8`,
				colors: {},
			};
		},
		methods: {
			renderColors() {
				this.colors = {
					fonts: this.inputToArrayOfObjects(this.fonts),
					backgrounds: this.inputToArrayOfObjects(this.backgrounds),
				};
			},
			inputToArrayOfObjects(input) {
				return input.split('\n').map((color) => {
					const attributes = color.split(':');
					return {
						name: attributes[0].trim(),
						value: attributes[1].trim().replace(/\;/g, ''),
					};
				});
			},
		},
		mounted() {
			this.renderColors();
		},
	};
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
	}

	label {
		display: block;
	}

	textarea {
		margin-bottom: 40px;
	}

	.container {
		display: flex;
		flex-direction: column;
	}

	.nav {
		display: flex;
		width: 100%;
	}

	.main {
		display: flex;
	}

	.main__data {
		max-width: 300px;
	}

	.main__render {
		flex: 1;
	}
</style>
