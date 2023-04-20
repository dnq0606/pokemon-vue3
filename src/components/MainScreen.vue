<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>

      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>

      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>

      <button @click="onStart(100)">
        <span>10x10</span>
        <span>SupperHard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(value) {
      this.$emit("onStart", { totalOfBlocks: value });
    },
  },
};
</script>
<style scoped>
.screen {
  width: 100vw;
  height: 100vh;
  background-color: var(--black);
  color: var(--white);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1 {
  font-size: 3.6rem;
  padding: 1rem;
}
h3 {
  font-size: 1.6rem;
  padding: 1rem;
}

button {
  background-color: #eee;
  border: none;
  padding: 1rem;
  font-size: 1rem;
  width: auto;
  border-radius: 1rem;
  color: lightcoral;
  box-shadow: 0 0.4rem #dfd9d9;
  cursor: pointer;
  margin: 10px;
  text-align: center;
}

button:active {
  color: white;
  box-shadow: 0 0.2rem #dfd9d9;
  transform: translateY(0.2rem);
}

button:hover:not(:disabled) {
  background: lightcoral;
  color: white;
  text-shadow: 0 0.1rem #bcb4b4;
}

button:disabled {
  cursor: auto;
  color: rgb(128, 128, 128);
}

button span {
  padding: 3px;
  font-weight: 600;
}
</style>
