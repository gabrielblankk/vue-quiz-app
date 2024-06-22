<script setup>
import { defineProps, computed, defineEmits } from 'vue'
import Option from '../components/Option.vue'
import gsap from 'gsap';


const props = defineProps(['currentQuestion', 'color'])

const emit = defineEmits(['optionSelected'])

const options = computed(() => props.currentQuestion.options)
function animateEnter(el) {
  el.style.opacity = '0'
  el.style.transform = 'translateY(20px)'

  gsap.to(el, {
    opacity: 1,
    y: '0px',
    duration: 0.2
  })
}

function animateLeave(el) {
  gsap.to(el, {
    opacity: 0,
    y: '-20px',
    duration: 0,
    transition: 0.2
  })
}
</script>

<template>
  <div class="question-container">
    <Transition
      mode="out-in"
      @enter="animateEnter"
      @leave="animateLeave"
    >
      <h1 :key="props.currentQuestion">{{ props.currentQuestion.text }}</h1>
    </Transition>

    <Option v-for="option in options"
      :key="option.id"
      :option="option"
      :color="props.color"
      @click="emit('optionSelected', option.isCorrect)"
    />
  </div>
</template>

<style scoped>
.question-container {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
}

h1 {
  font-size: 40px;
  font-weight: lighter;
}
</style>