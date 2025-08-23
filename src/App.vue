<script setup>
import { ref, computed } from 'vue';
import Card from './components/Card.vue';
import Icon from './components/Icon.vue'

const cardsModels = ref([]);
const score = ref(0);
const isEditModeActive = ref(false);
const isGameStopped = ref(false);
const gameLetter = ref('A')

const stopIconColor = computed(() => {
  return isGameStopped.value ? "var(--color-main)" : "var(--color-main-off)"
})

const editIconColor = computed(() => {
  return isEditModeActive.value ? "var(--color-main)" : "var(--color-main-off)"
})

function addCard() {
  cardsModels.value.push({ title: '', answer: '', points: undefined });
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

function scorePoints() {
  for (let card of cardsModels.value) {
    score.value += card.points ? card.points : 0
    card.points = undefined
  }
  isGameStopped.value = false;
  clearInputs();
}

function chooseRandomLetter() {
  let alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  gameLetter.value = alphabet[Math.floor(Math.random() * alphabet.length)];
}
</script>

<template>
  <div id="app">
    <h1 id="main-title">
      Le Petit Bac
    </h1>
    
    <div id="tools-area">
      <button class="tool" id="erase-btn" @click="chooseRandomLetter">
        <div id="random-letter">{{ gameLetter.toUpperCase() }}</div>
      </button>
      <button class="tool" id="toggle-edit-btn" @click="() => { isEditModeActive = !isEditModeActive }">
        <Icon name="pencil" width="40" height="40" :color="editIconColor" />
      </button>
      <button class="tool" id="stop-btn" @click="() => { isGameStopped = !isGameStopped }">
        <Icon name="stop" width="40" height="40" :color="stopIconColor" />
      </button>
    </div>

    <div id="card-area">
      <div class="card-row" v-for="(card, idx) in cardsModels">
        <Card v-model:title="card.title" v-model:answer="card.answer" v-model:points="card.points"
          :isPointsAreaVisible="isGameStopped" @points="" />
        <Icon v-if="isEditModeActive" name="X" color="red" width="10vw" height="10vw" @click="deleteCard(idx)" />
      </div>
    </div>

    <button v-if="!isGameStopped" class="centered-btn" @click="addCard">+</button>
    <button v-if="isGameStopped" class="centered-btn" id="score-it-btn" @click="scorePoints">Score it!</button>
    <div id="score-area">
      <span id="score-text">Your score: {{ score }}</span>
      <div id="score-buttons">
        <button v-if="isEditModeActive" class="score-adjust-btn" @click="() => scoreAdd(1)">+</button>
        <button v-if="isEditModeActive" class="score-adjust-btn" @click="() => scoreAdd(-1)">-</button>
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
  /*↓ To make it appear on top of cards: had a bug where placeholder has showing up through the tools bar*/
  z-index: 1000;
}

#random-letter{
  color: var(--color-main);
  font-size: 40px;
  font-family: "PatrickHand";
}

.tool {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  border-radius: 0;
  border-bottom: 3px solid grey;
  margin-top: -2vh;
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
  font-size: 5vh;
  font-family: "PatrickHand";
}

#score-buttons {
  display: flex;
  gap: 3vw;
}

.centered-btn {
  padding: 12px 32px;
  width: 60vw;
  margin: auto;
}
.score-adjust-btn{
  width: 8vw;
}

#score-it-btn{
  background: radial-gradient(circle, rgb(246 9 97) 30%,var(--color-main) 100%);
}
</style>