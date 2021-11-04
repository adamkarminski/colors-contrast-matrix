<template lang="">
	<div class="matrix">
		<div class="matrix__row">
			<div class="matrix__cell">Backgrounds \ Fonts</div>
			<div class="matrix__cell" v-for="font in colors.fonts">
				<div>
					<h4>{{ font.name }}</h4>
					<p>{{ font.value }}</p>
				</div>
			</div>
		</div>
		<div class="matrix__row" v-for="bg in colors.backgrounds">
			<div class="matrix__cell">
				<div>
					<h4>{{ bg.name }}</h4>
					<p>{{ bg.value }}</p>
				</div>
			</div>
			<div class="matrix__cell" v-for="f in colors.fonts">
				<MatrixCell :font="f" :background="bg"></MatrixCell>
			</div>
		</div>
	</div>
</template>

<script>
	import MatrixCell from './MatrixCell.vue';

	export default {
		components: { MatrixCell },
		props: {
			colors: Object,
		},
	};
</script>
<style>
	.matrix {
		display: flex;
		flex-direction: column;
		width: 100%;
	}

	.matrix__row {
		border-bottom: 1px solid #efefef;
		display: flex;
		flex: 1;
		margin-bottom: 16px;
	}

	.matrix__cell {
		align-items: center;
		display: flex;
		flex-direction: column;
		flex: 1;
		height: 100px;
		justify-content: center;
		max-width: 300px;
		margin: 10px;
		text-align: center;
	}
</style>
