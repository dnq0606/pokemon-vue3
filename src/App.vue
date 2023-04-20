<!-- eslint-disable no-unused-vars -->
<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeSart($event)"
  ></main-screen>

  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onFinish($event)"
  />

  <result-screen
    v-if="statusMatch === 'result'"
    :second="timeFinish"
    @onSartAgain="onSartAgain"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
// eslint-disable-next-line no-unused-vars
import { shuffled } from "./utils/array";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        starteAt: null,
      },
      timeFinish: null,
    };
  },
  methods: {
    onHandleBeforeSart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(shuffled(cards))))
      );
      this.settings.starteAt = new Date().getTime();
      this.statusMatch = "match";
    },
    onFinish(time) {
      this.timeFinish = Math.abs(time - this.settings.starteAt) / 1000;
      this.statusMatch = "result";
    },
    onSartAgain() {
      this.statusMatch = "default";
    },
  },
};
</script>

<style scoped></style>
