<template>
  <div class="ctr">
    <Transition name="fade" mode="out-in">
      <Questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="QuestionAnswered"
      ></Questions>

      <Result v-else :results="results" :totalCorrect="totalCorrect"></Result>
    </Transition>

    <button
      type="button"
      class="reset-btn"
      @click="Reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Question.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              isCorrect: true,
            },
            {
              text: "3",
              isCorrect: false,
            },
            {
              text: "Fish",
              isCorrect: false,
            },
            {
              text: "5",
              isCorrect: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              isCorrect: false,
            },
            {
              text: "7",
              isCorrect: false,
            },
            {
              text: "6",
              isCorrect: true,
            },
            {
              text: "12",
              isCorrect: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              isCorrect: false,
            },
            {
              text: "a",
              isCorrect: true,
            },
            {
              text: "i",
              isCorrect: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    QuestionAnswered(isCorrect) {
      if (isCorrect) {
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    Reset() {
      this.totalCorrect = this.questionsAnswered = 0;
    },
  },
};
</script>

<style>
</style>
