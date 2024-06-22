<script setup>
import { defineProps } from 'vue'
import { useRouter } from 'vue-router'


const router = useRouter()

const { quiz } = defineProps(['quiz'])
</script>

<template>
  <div class="quiz-card" @click="router.push(`/quiz/${quiz.id}`)">
    <img :src="quiz.img">

    <h1>{{ quiz.name }}</h1>
    
    <p>{{ quiz.questions.length }} Questions</p>
  </div>
</template>

<style scoped>
.quiz-card { 
  display: flex;
  flex-direction: column;
  margin-right: 20px;
  margin-bottom: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px #aaa;
  cursor: pointer;
  transition: 0.2s;
}

.quiz-card:hover {
  transform: scale(1.05);
}

.quiz-card:active {
  transform: scale(1);
}

img {
  width: 300px;
  height: 175px;
  object-fit: cover;
  margin: 0;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
}

h1, p {
  margin: 10px;
}
</style>