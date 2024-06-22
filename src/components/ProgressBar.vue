<script setup>
import { defineProps, computed } from 'vue'


const props = defineProps(['numberOfQuestions', 'currentQuestionNumber', 'color'])

const progressFill = computed(() => `${Math.floor((props.currentQuestionNumber) * (100 / props.numberOfQuestions ))}%`) 
</script>

<template>
  <h1>Question {{ props.currentQuestionNumber }}/{{ props.numberOfQuestions }}</h1>

  <div class="progress-bar" :style="{ borderColor: props.color.light }">
    <div class="fill" :style="{ backgroundColor: props.color.dark, width: progressFill }"></div>
  </div>
</template>

<style scoped>
h1 {
  font-size: 40px;
  font-weight: normal;
}

.progress-bar {
  border: solid 2px;
  width: 215px;
  height: 35px;
  border-radius: 100px;
}

.fill {
  height: 100%;
  border-radius: 100px;
  transition: 0.4s;
}
</style>