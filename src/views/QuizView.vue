<script setup>
import { useRoute } from 'vue-router'
import { ref, computed } from 'vue'
import ProgressBar from '../components/ProgressBar.vue'
import Question from '../components/Question.vue'
import Result from '../components/Result.vue'
import q from '../data/quizzes.json'
import gsap from 'gsap'


const route = useRoute()

const quiz = q.find(q => q.id === Number(route.params.id))

const questionIndex = ref(0)

const correctAnswers = ref(0)

const currentQuestion = computed(() => quiz.questions[questionIndex.value])
  
function nextQuestion(isCorrect) {
  questionIndex.value++
  
  if (isCorrect) correctAnswers.value++
}

function animateEnter(el) {
  el.style.opacity = '0'
  el.style.transform = 'scale(0)'

  gsap.to(el, {
    scale: 1,
    opacity: 1,
    duration: 0.5,
    delay: 0.3
  })
}

function animateLeave(el) {
  gsap.to(el, {
    x: '-20px',
    opacity: 0,
    duration: 0,
    transition: 0.3
  })
}
</script>

<template>
  <div>
    <header>
      <h1>{{ quiz.name }}</h1>

      <ProgressBar  
        :numberOfQuestions="quiz.questions.length" 
        :currentQuestionNumber="questionIndex"
        :color="quiz.color"
      />
    </header>

    <Transition 
      name="questions-animation"
      @leave="animateLeave"
    >
      <Question 
        v-if="questionIndex < quiz.questions.length"
        :currentQuestion="currentQuestion"
        :color="quiz.color"
        @optionSelected="nextQuestion"  
      />
    </Transition>
      
    <Transition 
      name="result-animation" 
      appear
      @enter="animateEnter"
    >
      <Result
        v-if="questionIndex >= quiz.questions.length"
        :correctAnswers="correctAnswers"
        :numberOfQuestions="quiz.questions.length"
        :color="quiz.color"
      />
    </Transition>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 220px;
}

header h1 {
  font-size: 60px;
  font-weight: bolder;
  margin-bottom: 20px;
}
</style>