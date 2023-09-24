<script setup>
import { defineProps } from "vue";

const { questionStatus, barPercentage } = defineProps([
  "questionStatus",
  "barPercentage",
]);
</script>

<template>
  <header>
    <h4>Question {{ questionStatus }}</h4>
    <div class="bar">
      <div class="completion" :style="{width:barPercentage}"></div>
    </div>
  </header>
</template>

<style scoped>
header {
  margin-top: 20px;
}

h4 {
  font-size: 30px;
}

.bar {
  width: 300px;
  height: 50px;
  border: 3px solid bisque;
  border-radius: 40px;
}

.completion {
  height: 100%; 
  background-color: rgb(10, 240, 163);;
  border-radius: 40px;
}
</style>
