<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const cardsModels = ref([]);

function addCard() {
  cardsModels.value.push({ title: '', answer: '' });
}

function clearInputs() {
  cardsModels.value.forEach(card => {
    card.answer = '';
  });
}
</script>

<template>
  <div id="app">
    <h1 id="main-title">
      Le Petit Bac
    </h1>

    <div id="card-area">
      <Card v-for="(card, idx) in cardsModels" :key="idx" v-model:title="card.title" v-model:answer="card.answer" />
    </div>

    <div id="button-area">
      <button class="bottom-btn" @click="addCard">+</button>
      <button v-if="cardsModels.length > 0" class="bottom-btn" id="clear-inputs-btn" @click="clearInputs">Clear</button>
    </div>
  </div>
</template>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
}

#main-title {
  background-color: var(--color-main);
  font-size: 2rem;
  text-align: center;
  font-family: "FingerPaint";
  margin: 0;
}

#card-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  margin-top: 2rem;
}

#button-area {
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

#clear-inputs-btn {
  background-color: rgba(255, 67, 67, 0.667);
}
</style>