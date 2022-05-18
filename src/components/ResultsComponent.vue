<template>
	<div class="result">
		<div class="title">
			{{computedResult.title}}
		</div>

		<div class="desc">
			{{computedResult.desc}}
		</div>
	</div>
</template>

<script>
export default {
	
	props: {
		results: Array,
		totalCorrect: Number
	},

	computed: {
		computedResult() {

			const r = this.results.find(result => result.min <= this.totalCorrect && result.max >= this.totalCorrect);
			return r ? r : this.result[0];
		}
	}
	
}
</script>