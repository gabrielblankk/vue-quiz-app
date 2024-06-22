<script setup>
import QuizCard from '../components/QuizCard.vue'
import q from '../data/quizzes.json'
import { ref, computed } from 'vue'
import gsap from 'gsap'

const search = ref('')

const quizzes = computed(() => q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase())))

function animateEnter(el) {
  el.style.opacity = '0'
  el.style.transform = 'translateY(-20px)'
  
  gsap.to(el, {
    y: '0px',
    opacity: 1,
    duration: 0.3,
    transition: 0,
    delay: el.dataset.index * 0.05,
    onComplete: () => {
      el.style.opacity = ''
      el.style.transform = ''
      el.style.transition = ''
    }      
  })
}

function animateLeave(el) {
  gsap.to(el, {
    y: '-20px',
    opacity: 0,
    duration: 0,
    transition: 0.3,
    position: 'absolute'
  })
}

</script>

<template>
  <div>
    <header>
      <h1>Quizzes</h1>

      <input v-model="search" type="text" placeholder="Search...">
    </header>

    <div class="quizzes-container">
      <TransitionGroup 
        name="cards-animation" 
        @enter="animateEnter"
        @leave="animateLeave"
        appear
      >
        <QuizCard 
          v-for="(quiz, index) in quizzes" 
          :key="quiz.id"
          :quiz="quiz"
          :data-index="index"
        />
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 40px;
  display: flex;
  align-items: center;
  height: 100px;
}

header h1 {
  font-size: 60px;
  margin-right: 40px;
}

header input {
  height: 40px;
  padding: 20px;
  font-size: 20px;
  background-color: #ddd;
  border: none;
  border-radius: 20px;
}

.quizzes-container {
  display: flex;
  flex-wrap: wrap;
}
</style>