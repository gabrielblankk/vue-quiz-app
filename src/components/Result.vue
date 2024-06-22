<script setup>
import { defineProps } from 'vue'
import { useRouter } from 'vue-router'


const router = useRouter()

const props = defineProps(['correctAnswers', 'numberOfQuestions', 'color'])
</script>

<template>
  <div class="result-container">
    <p>Your results...</p>

    <h1>{{ correctAnswers }}/{{ numberOfQuestions }}</h1>
    
    <button @click="router.push('/')" :style="{ backgroundColor: props.color.light }">Go back</button>
  </div>
</template>

<style scoped>
.result-container {
  margin-top: 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

p {
  font-size: 60px;
  font-weight: lighter;
}

h1 {
  font-size: 100px;
  font-weight: bolder;
}

button {
  border: none;
  font-size: 20px;
  padding: 5px 20px;
  border-radius: 100px;
  transition: 0.2s;
  cursor: pointer;
}

button:hover {
  transform: scale(1.05);
}
</style>