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
	import { computed } from 'vue';

	export default {
		
		props: {
			results: Array,
			totalCorrect: Number
		},

		setup(props) {
			const computedResult = computed(() => {

				const r = props.results.find(result => result.min <= props.totalCorrect && result.max >= props.totalCorrect);
				return r ? r : props.result[0];
			});

			return {computedResult};
		}

	};
</script>