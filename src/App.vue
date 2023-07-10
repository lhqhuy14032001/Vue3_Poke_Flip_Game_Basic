<template>
  <div class="screen">
    <main-screen
      v-if="stateMatch === 'default'"
      @onStart="onToggleScreen($event)"
    />
    <interact-screen
      v-if="stateMatch === 'match'"
      @onBackToMainScreen="onBackToMainScreen"
      :cardsContext="settings.cardsContext"
      @onFinish="onGetResult"
    />
    <result-screen
      v-if="stateMatch === 'result'"
      :timer="timer"
      @onStartAgain="stateMatch = 'default'"
    />
  </div>
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
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
        timer: 0,
      },
      stateMatch: "default",
    };
  },
  methods: {
    onToggleScreen(config) {
      const settings = this.settings;
      settings.totalOfBlocks = config.totalOfBlocks;
      const firtsCards = Array.from(
        { length: settings.totalOfBlocks / 2 },
        (_, i) => {
          return i + 1;
        }
      );
      const secondCards = [...firtsCards];
      const cards = [...firtsCards, ...secondCards];
      settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
      settings.startedAt = new Date().getTime();
      this.stateMatch = "match";
    },
    onBackToMainScreen() {
      this.stateMatch = "default";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;

      this.stateMatch = "result";
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  min-height: 100vh;
  /* display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column; */
}
</style>
