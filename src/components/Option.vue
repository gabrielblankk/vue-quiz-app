<script setup>
  import { defineProps } from 'vue'


  const props = defineProps(['option', 'color'])
</script>

<template>
  <div class="option" :style="{ backgroundColor: props.color.light }">
    <label :style="{ backgroundColor: props.color.dark }">{{ option.label }}</label>
    
    <p>{{ option.text }}</p>
  </div>
</template>

<style scoped>
.option {
  display: flex;
  align-items: center;
  margin-top: 20px;
  transition: 0.2s;
  cursor: pointer;
}

.option:hover {
  transform: scale(1.05);
}

.option:active {
  transform: scale(1);
}

label {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 60px;
  width: 60px;
  margin-right: 30px;
  font-size: 40px;
  font-weight: bolder;
}

p {
  font-size: 30px;
  font-weight: normal;
}
</style>