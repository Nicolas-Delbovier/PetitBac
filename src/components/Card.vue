<template>
  <div class="card">
    <div class="card-top">
      <input type="text" class="card-input" placeholder="Title" />
    </div>
    <div class="card-bottom">
      <input type="text" class="card-input" placeholder="Answer" />
    </div>
  </div>
</template>

<script setup>
// No script logic needed for now
</script>

<style scoped>

.card {
  width: 300px;
  height: 200px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
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
  width: 80%;
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #ddd;
  font-size: 1rem;
}
</style>