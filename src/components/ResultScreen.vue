<template>
  <div class="result">
    <div class="result__title">
      <img src="../assets/images/star.png" alt="icon" />
      <h1>Congratulations</h1>
      <img src="../assets/images/star.png" alt="icon" />
    </div>
    <div class="result__seconds">
      <span>{{ second }} seconds</span>
    </div>
    <div class="result__button">
      <button @click="$emit('onSartAgain')">Start Again</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    second: {
      type: Number,
      required: true,
    },
  },
};
</script>
<style lang="css" scoped>
.result {
  width: 100%;
  height: 100vh;
  color: var(--white);
  background-color: var(--black);
}
.result__title {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 26%;
}
.result__title img {
  width: 60px;
  height: 60px;
  margin: 0 12px;
}
.result__title h1 {
  font-size: 3.6rem;
}

.result__seconds,
.result__button {
  display: flex;
  justify-content: center;
  align-items: center;
}

.result__seconds {
  font-size: 2.6rem;
  margin: 20px 0;
}

button {
  position: relative;
  display: inline-block;
  margin: 15px;
  padding: 15px 30px;
  text-align: center;
  font-size: 18px;
  letter-spacing: 1px;
  text-decoration: none;
  color: var(--blue);
  background: transparent;
  cursor: pointer;
  transition: ease-out 0.5s;
  border: 2px solid var(--blue);
  border-radius: 10px;
  box-shadow: inset 0 0 0 0 var(--blue);
  font-weight: 600;
}

button:hover {
  color: white;
  box-shadow: inset 0 -100px 0 0 var(--blue);
}

button:active {
  transform: scale(0.9);
}
</style>
