<!-- eslint-disable no-unused-vars -->
<template>
  <main-screen
    v-if="statusMatch === 'default'"
    v-on:onStart="onHandleBeforeSart($event)"
  ></main-screen>

  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
// eslint-disable-next-line no-unused-vars
import { shuffled } from "./utils/array";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
  },
  data() {
    return {
      statusMatch: "default",
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        starteAt: null,
      },
    };
  },
  methods: {
    onHandleBeforeSart(config) {
      console.log("running method onHandleBeforeSart", config);
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
  },
};
</script>

<style scoped></style>
