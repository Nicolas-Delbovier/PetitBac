<script setup>
import { ref } from 'vue'
import Card from './components/Card.vue'

// Cards state
const cards = ref([])

function addCard() {
  cards.value.push({})
}
</script>

<template>
  <div id="app">
    <!-- Title -->
    <div class="main-title">
      Petit Bac
    </div>

    <!-- Card Area -->
    <div class="card-area">
      <Card v-for="(card, idx) in cards" :key="idx" />
    </div>

    <!-- Add Card Button -->
    <div class="button-area">
      <button class="add-card-btn" @click="addCard">Add Card</button>
    </div>
  </div>
</template>

<style scoped>

#app {
  display: flex;
  flex-direction: column;
}

.main-title {
  background-color: var(--color-main);
  font-size: 2rem;
  text-align: center;
  font-family: "Gagalin";
}

.card-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 200px;
  gap: 2rem;
  margin-top: 2rem;
}

.button-area {
  display: flex;
  justify-content: center;
  margin-top: 24px;
}

.add-card-btn {
  background: var(--card-main);
  border: none;
  padding: 12px 32px;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.add-card-btn {
  background-color: var(--color-main);
  color: white;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
