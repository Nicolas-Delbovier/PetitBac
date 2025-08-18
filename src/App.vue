<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';
import TrashIcon from './components/TrashIcon.vue'

const cardsModels = ref([]);
const score = ref(0);
const isCardDeleteVisible = ref(false);
const isGameStopped = ref(false);

function addCard() {
  cardsModels.value.push({ title: '', answer: '' });
}

function clearInputs() {
  cardsModels.value.forEach(card => {
    card.answer = '';
  });
}

function scoreAdd(i) {
  score.value = Math.max(score.value + i, 0);
}

function deleteCard(i) {
  if (i > -1) {
    cardsModels.value.splice(i, 1);
  }
}
</script>

<template>
  <div id="app">
    <h1 id="main-title">
      Le Petit Bac
    </h1>

    <div id="tools-area">
      <button class="tool" id="toggle-delete-btn" @click="() => { isCardDeleteVisible = !isCardDeleteVisible }">Toggle
        delete</button>
      <button class="tool" id="stop-btn" @click="() => { isGameStopped = !isGameStopped }">STOP</button>
    </div>

    <div id="card-area">
      <div class="card-row" v-for="(card, idx) in cardsModels">
        <Card v-model:title="card.title" v-model:answer="card.answer" :isPointsAreaVisible="isGameStopped" />
        <TrashIcon v-if="isCardDeleteVisible" iconColor="red" width="10vw" height="10vw" @click="deleteCard(idx)" />
      </div>
    </div>

    <div id="button-area">
      <button class="bottom-btn" @click="addCard">+</button>
      <button v-if="cardsModels.length > 0" class="bottom-btn" id="clear-inputs-btn" @click="clearInputs">Clear</button>
    </div>
    <div id="score-area">
      <span id="score-text">Your score: {{ score }}</span>
      <div id="score-buttons">
        <button class="increase-btn" @click="() => scoreAdd(1)">+</button>
        <button class="decrease-btn" @click="() => scoreAdd(-1)">-</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  gap: 2vh;
}

#main-title {
  background-color: var(--color-main);
  font-size: 2rem;
  text-align: center;
  font-family: "FingerPaint";
  margin: 0;
}

#tools-area {
  display: flex;
  position: sticky;
  top: 0px;
  height: 10vh;
  border-bottom: 3px solid white;
}

.tool {
  flex: 1;
}

#card-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  margin-top: 2rem;
}

.card-row {
  display: flex;
  gap: 5vw;
}

#button-area {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 24px;
}

#score-area {
  display: flex;
  gap: 3vw;
  justify-content: center;
}

#score-text {
  color: var(--color-main);
  font-size: large;
}

#score-buttons {
  display: flex;
  gap: 3vw;
}

.bottom-btn {
  padding: 12px 32px;
  width: 60vw;
}

.increase-btn {
  background-color: green;
  padding: 5px 10px;
}

.decrease-btn {
  background-color: red;
  padding: 5px 10px;
}


#clear-inputs-btn {
  background-color: rgba(255, 67, 67, 0.667);
}
</style>