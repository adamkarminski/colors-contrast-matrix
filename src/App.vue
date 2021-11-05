<template>
	<div class="container">
		<nav class="nav">
			<h1>Colors Contrast Matrix</h1>
		</nav>
		<div class="main">
			<div class="main__data">
				<span>Format:</span>
				<pre class="main__data__format">[COLOR NAME]: [#HEX]</pre>

				<label class="main__data__font__label" for="main__data__font">Fonts</label>
				<textarea v-model="fonts" name="main__data__font" class="main__data__input" cols="30" rows="10">
				</textarea>

				<label class="main__data__background__label" for="main__data__background">Backgrounds</label>
				<textarea
					v-model="backgrounds"
					name="main__data__background"
					class="main__data__input"
					cols="30"
					rows="10"
				>
				</textarea>

				<button class="main__data__confirm" @click="renderColors">Rerender matrix</button>

				<div role="footer" class="footer">
					<p class="caption">
						Created by <a href="https://github.com/adamkarminski" target="_blank">Adam Karmiński</a> from
						<a href="https://bethink.tech" target="_blank">Bethink</a>
					</p>
					<p>
						<a href="https://github.com/adamkarminski/colors-contrast-matrix" target="_blank">
							<img
								src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png"
								alt="GitHub's logo"
								title="GitHub repo"
								width="30"
								height="30"
							/>
						</a>
					</p>
				</div>
			</div>
			<div class="main__render">
				<ColorsMatrix :colors="colors" />
			</div>
		</div>
	</div>
</template>

<script>
	import ColorsMatrix from './components/ColorsMatrix.vue';

	const FONTS_DEFAULTS = `gray900: #1F2534\ngray800: #434A5A\ngray700: #6F7285\ngray600: #868C9E\ngray500: #A7ACBD\ngray400: #BDC1CD\ngray300: #CDD0DA\ngray200: #E6E8EE\ngray100: #EFF0F3\ngray50: #F6F6F8`;

	const BACKGROUNDS_DEFAULTS = `gray900: #1F2534\ngray800: #434A5A\ngray700: #6F7285\ngray600: #868C9E\ngray500: #A7ACBD\ngray400: #BDC1CD\ngray300: #CDD0DA\ngray200: #E6E8EE\ngray100: #EFF0F3\ngray50: #F6F6F8`;

	export default {
		components: { ColorsMatrix },
		data() {
			return {
				fonts: FONTS_DEFAULTS,
				backgrounds: BACKGROUNDS_DEFAULTS,
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
				return input
					.split('\n')
					.filter((color) => {
						return color.indexOf(':') > -1;
					})
					.map((color) => {
						const attributes = color.replace(/\;/g, '').split(':');

						return {
							name: attributes[0].trim(),
							value: attributes[1].trim(),
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
		padding: 0 24px;
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

	.main__data__format {
		margin-top: 0;
		margin-bottom: 24px;
	}

	.main__data__confirm {
		border: 0;
		border-radius: 100px;
		background-color: #2c3e50;
		color: #fff;
		cursor: pointer;
		display: block;
		font-size: 1rem;
		font-weight: bold;
		padding: 12px 20px;
		transition: background-color 0.2s;
		width: 100%;
	}

	.main__data__confirm:hover {
		background-color: #6d7884;
	}

	.main__render {
		flex: 1;
		padding: 0 24px;
	}

	.footer {
		margin-top: 40px;
	}

	.caption {
		font-size: 0.8rem;
	}
</style>
