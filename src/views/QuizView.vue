<script setup>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import Result from "../components/Result.vue";
import { useRoute } from "vue-router";
import { ref, watch, computed } from "vue";
import quizes from "../data/quizes.json";

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizes.find((q) => q.id == quizId);
const currentQuestionIndex = ref(0);
const numberOfCorrectAnswers = ref(0);
const showresults = ref(false)

// const questionStatus = ref(`${currentQuestionIndex.value + 1}/${quiz.questions.length}`);

// watch(() => currentQuestionIndex.value,() => {
//     questionStatus.value = `${currentQuestionIndex.value + 1}/${quiz.questions.length}`;
// })

const questionStatus = computed(() => {
  return `${currentQuestionIndex.value}/${quiz.questions.length}`;
});

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAnswers.value++;
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showresults.value = true;
  }

  currentQuestionIndex.value++;
};
</script>

<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
        v-if="!showresults"
      />
      <Result :quizQuestionLength="quiz.questions.length" :numberOfCorrectAnswers="numberOfCorrectAnswers" v-else/>
    </div>
  </div>
</template>
