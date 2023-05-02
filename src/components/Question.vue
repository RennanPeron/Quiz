<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <TransitionGroup name="fade">
      <div
        class="single-question"
        v-for="(question, qIndex) in questions"
        :key="question.q"
        v-show="qIndex === questionsAnswered"
      >
        <div class="question">
          {{ question.q }}
        </div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="SelectAnswer(answer.isCorrect)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ["questions", "questionsAnswered"],
  emits: ["question-answered"],
  methods: {
    SelectAnswer(isCorrect) {
      this.$emit("question-answered", isCorrect);
    },
  },
};
</script>
