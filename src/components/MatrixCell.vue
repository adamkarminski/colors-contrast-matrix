<template lang="">
	<div class="cell">
		<div :style="{ backgroundColor: this.background.value, color: this.font.value }" class="cell__visualization">
			<span class="cell__visualization__contrast">{{ contrast }}</span>
		</div>
		<div class="cell__caption">
			F {{ font.name }} / BG {{ background.name }} / C {{ contrast }} /
			<span :class="scoreClass">S {{ score }}</span>
		</div>
	</div>
</template>
<script>
	import * as wcag from 'wcag-contrast';

	export default {
		props: {
			font: Object,
			background: Object,
		},
		computed: {
			contrast() {
				return wcag.hex(this.font.value, this.background.value).toFixed(2);
			},
			score() {
				return wcag.score(this.contrast);
			},
			scoreClass() {
				return `score-${this.score.replace(/\s+/g, '').toLowerCase()}`;
			},
		},
	};
</script>
<style>
	.cell {
		align-items: center;
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		height: 100%;
	}

	.cell__visualization {
		align-items: center;
		border: 1px solid #efefef;
		display: flex;
		flex: 1;
		justify-content: center;
		margin-bottom: 16px;
		width: 100%;
	}

	.cell__visualization__contrast {
		font-size: 1.75rem;
		font-weight: 700;
	}

	.cell__caption {
		color: #454545;
		font-size: 0.75rem;
	}

	.score-aaa {
		color: green;
	}

	.score-aa {
		color: blue;
	}

	.score-aalarge {
		color: orange;
	}

	.score-fail {
		color: red;
	}
</style>
