<script setup>
import { ref, computed } from 'vue';
import Card from './components/Card.vue';
import Icon from './components/Icon.vue'

const cardsModels = ref([]);
const score = ref(0);
const isCardDeleteVisible = ref(false);
const isGameStopped = ref(false);

const stopIconColor = computed(() => {
  return isGameStopped.value ? "var(--color-main)" : "var(--color-main-off)"
})

const toggleDeleteIconColor = computed(() => {
  return isCardDeleteVisible.value ? "var(--color-main)" : "var(--color-main-off)"
})

const eraseIconColor = computed(() => {
  const hasAnswers = cardsModels.value.some(card => card.answer !== '');
  return hasAnswers ? "var(--color-main)" : "var(--color-main-off)";
});

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

function scorePoints(){
  for(let card of cardsModels.value){
    score.value += card.points ? card.points : 0
    card.points = undefined
  }
  isGameStopped.value = false;
  clearInputs();
}
</script>

<template>
  <div id="app">
    <h1 id="main-title">
      Le Petit Bac
    </h1>

    <div id="tools-area">
      <button class="tool" id="erase-btn" @click="clearInputs">
        <Icon name="eraser" width="40" height="40" :color="eraseIconColor" />
      </button>
      <button class="tool" id="toggle-delete-btn" @click="() => { isCardDeleteVisible = !isCardDeleteVisible }">
        <Icon name="trash" width="40" height="40" :color="toggleDeleteIconColor" />
      </button>
      <button class="tool" id="stop-btn" @click="() => { isGameStopped = !isGameStopped }">
        <Icon name="stop" width="40" height="40" :color="stopIconColor" />
      </button>
    </div>

    <div id="card-area">
      <div class="card-row" v-for="(card, idx) in cardsModels">
        <Card v-model:title="card.title" v-model:answer="card.answer" v-model:points="card.points"
          :isPointsAreaVisible="isGameStopped" @points="" />
        <Icon v-if="isCardDeleteVisible" name="X" color="red" width="10vw" height="10vw" @click="deleteCard(idx)" />
      </div>
    </div>

    <button v-if="!isGameStopped" class="centered-btn" @click="addCard">+</button>
    <button v-if="isGameStopped" class="centered-btn" @click="scorePoints">Score it!</button>
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
  /*↓ To make it appear on top of cards: had a bug where placeholder has showing up through the tools bar*/
  z-index: 1000;
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
  font-size: large;
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

.increase-btn {
  background-color: green;
  padding: 5px 10px;
}

.decrease-btn {
  background-color: red;
  padding: 5px 10px;
}
</style>