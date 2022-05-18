<template>
	<div class="questions-ctr">
			<div class="progress">
				<div class="bar" :style="computedStyle"></div>
				<div class="status">{{currentQuestion}} out of {{questions.length}} questions answered</div>
			</div>

			<transition name="fade" appear>
				<div class="single-question" v-if="activeQuestion" >
					<div class="question">
						{{activeQuestion.q}}
					</div>

					<div class="answers">
						<div
							class="answer"
							v-for="answer in activeQuestion.answers"
							:key="answer.text"
							@click="answerSelected(answer.is_correct)"
						>
							{{answer.text}}
						</div>
					</div>
				</div>
			</transition>
		</div>
</template>

<script>
	import { computed } from 'vue';

	export default {
		name: 'QuestionsComponent',

		props: {
			questions: Array,
			currentQuestion: Number
		},

		setup(props, {emit}) {

			function answerSelected(correct) {
				emit('answer-selected', correct);
			}

			const activeQuestion = computed(() => {
				const q = props.questions[props.currentQuestion];

				return q ? q : null;
			});

			const computedStyle = computed(() => {

				const p = (props.currentQuestion * 100) / props.questions.length;
				return {
					width: `${p}%`
				};
			});

			return { answerSelected, activeQuestion, computedStyle };
		}
		/*props: {
			questions: Array,
			currentQuestion: Number
		},

		emits: ['answer-selected'],

		methods: {
			answerSelected(correct) {
				this.$emit('answer-selected', correct);
			}
		},

		computed: {
			activeQuestion() {
				const q = this.questions[this.currentQuestion];

				return q ? q : null;
			},

			computedStyle() {

				const p = (this.currentQuestion * 100) / this.questions.length;
				return {
					width: `${p}%`
				};
			}
		}*/
	}

</script>
