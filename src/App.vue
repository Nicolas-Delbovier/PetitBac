<script setup>
import { ref } from 'vue'
import Card from './components/Card.vue'

// Cards state
const cards = ref([])

function addCard() {
  cards.value.push({})
}

function clearInputs(){
  
}
</script>

<template>
  <div id="app">
    <!-- Title -->
    <h1 class="main-title">
      Le Petit Bac
    </h1>

    <!-- Card Area -->
    <div class="card-area">
      <Card v-for="(card, idx) in cards" :key="idx" />
    </div>

    <!-- Add Card Button -->
    <div class="button-area">
      <button class="bottom-btn" @click="addCard">+</button>
      <button v-if="cards.length > 0" class="bottom-btn" id="clear-inputs-btn" @click="clearInputs">Clear</button>
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
  font-family: "FingerPaint";
  margin: 0;
}

.card-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  margin-top: 2rem;
}

.button-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 24px;
}

.bottom-btn {
  border: none;
  padding: 12px 32px;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  background-color: var(--color-main);
  color: white;
  width: 60%;
}

#clear-inputs-btn{
  background-color: #83a2ffaa;
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
