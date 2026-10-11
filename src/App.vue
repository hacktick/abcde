<script setup lang="ts">
import { ref } from 'vue'
import GameCanvas from './components/GameCanvas.vue'

const score = ref(0)
</script>

<template>
  <GameCanvas />
  <main class="hello">
    <h1>Hello World 👋</h1>
    <p>Vue 3 + Vite + TypeScript + three.js läuft. Hier entsteht ein Spiel.</p>
    <button type="button" @click="score++">Punkte: {{ score }}</button>
  </main>
</template>

<style scoped>
.hello {
  position: relative;
  text-align: center;
  padding: 2rem;
}

h1 {
  font-size: 3rem;
  margin: 0 0 0.5rem;
}

p {
  opacity: 0.75;
  margin: 0 0 1.5rem;
}

button {
  font: inherit;
  font-size: 1.1rem;
  padding: 0.7rem 1.4rem;
  border: 0;
  border-radius: 0.6rem;
  background: #42b883;
  color: #0c1a14;
  cursor: pointer;
  transition: transform 0.1s ease;
}

button:active {
  transform: scale(0.96);
}
</style>
