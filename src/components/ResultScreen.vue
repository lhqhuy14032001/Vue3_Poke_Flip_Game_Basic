<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <p class="play-again" @click="onStartAgain">Start Again</p>
  </div>
</template>

<script>
export default {
  props: {
    timer: { type: Number, require: true },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: #ffff;
}
.screen h1 {
  font-size: 72px;
}
.screen p {
  font-size: 32px;
}
.screen .play-again {
  color: rgb(255, 196, 0);
}
.screen .play-again:hover {
  text-decoration: underline;
  cursor: pointer;
}
</style>
