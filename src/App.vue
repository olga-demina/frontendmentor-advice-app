<script setup>
import { onMounted, reactive } from 'vue';

const state = reactive({ adviceNumber: 0, adviceText: "" });

onMounted(() => {
  fetchRandomAdvice();
})

async function fetchRandomAdvice() {
  const result = await (await fetch("https://api.adviceslip.com/advice")).json();
  state.adviceNumber = result.slip.id;
  state.adviceText = result.slip.advice;
}

</script>

<template>

  <main>
    <div class="container">
      <div class="card">
        <h3 class="advice-number">
          Advice #{{state.adviceNumber}}
        </h3>
        <p class="advice">"{{state.adviceText}}"</p>

        <button @click="fetchRandomAdvice">Generate</button>
      </div>
    </div>
  </main>

</template>

<style scoped>

</style>
