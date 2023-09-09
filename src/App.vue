<template>
  <MainScreen
    v-if="isStart == false"
    @onStartGame="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="isStart == true"
    :cardContext="settings.cardContext"
    @onFinish="onGetResult"
  />
  <ResultScreen v-if="isEnd == true" :timer="timer" @onStartAgain="againGame" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";

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
      settings: {
        totalOfBlock: 0,
        cardContext: [],
        startedAt: null,
      },
      isStart: false,
      isEnd: false,
      timer: 0,
    };
  },
  methods: {
    startedMatch() {
      console.log("event ....");
      console.log(this.$refs.hello);
      this.count++;
    },
    onHandleBeforeStart(config) {
      console.log("running game before start", config);
      this.settings.totalOfBlock = config.totalOfBlock;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );

      const secondCards = [...firstCards];

      const cards = [...firstCards, ...secondCards];

      console.log(firstCards);
      console.log(cards);
      this.settings.cardContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();
      //data: ready
      this.isStart = true;
    },
    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt;
      // swich to result components
      this.isEnd = true;
    },
    againGame() {
      this.isStart = false;
      this.isEnd = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #353535;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
