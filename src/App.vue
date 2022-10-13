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
      <div class="advice">
        <h3 class="advice-number">
          Advice #{{state.adviceNumber}}
        </h3>
        <p class="advice-text">"{{state.adviceText}}"</p>

        <picture>
          <source srcset="@/assets/images/pattern-divider-desktop.svg" media="(min-width: 768px)">
          <img class="advice-divider sr-hidden" src="@/assets/images/pattern-divider-mobile.svg" alt="">
        </picture>

        <button class="btn-generate" @click="fetchRandomAdvice">
          <span class="sr-only">Generate new advice</span>
          <img src="@/assets/images/icon-dice.svg" alt="Dice">
        </button>
      </div>
    </div>
  </main>

</template>
  

