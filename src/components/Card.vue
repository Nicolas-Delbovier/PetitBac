<template>
  <div class="card">
    <div class="card-top">
      <input type="text" v-model="title" class="card-input" placeholder="|" />
    </div>
    <div class="card-bottom">
      <input type="text" v-model="answer" class="card-input" placeholder="|" />
    </div>
  </div>
</template>

<script setup>
const title = defineModel("title");
const answer = defineModel("answer");
</script>

<style scoped>
.card {
  width: 70%;
  height: 100px;
  display: flex;
  flex-direction: column;
  box-shadow: 5px 5px rgba(0, 0, 0, 0.5);
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid black;
}

.card-top {
  background: var(--color-main);
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-bottom {
  background: #fff;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-input {
  width: fit-content;
  padding: 6px;
  font-size: 1rem;
  font-weight: bold;
  background-color: transparent;
  color: white;
  border: 0;
  text-align: center;
}

.card-top>input {
  color: white;
}

.card-bottom>input {
  color: var(--color-main);
}

.card-top>input::placeholder {
  font-weight: bold;
  opacity: 0.5;
  color: white;
}

.card-bottom>input::placeholder {
  font-weight: bold;
  opacity: 0.5;
  color: var(--color-main);
}
</style>