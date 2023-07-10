<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        class="card"
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardContext="cardsContext"
        @onFlip="checkRule($event)"
      />
      <p class="btn__back" @click="onBackToMainScreen">Back to Home</p>
    </div>
  </div>
</template>

<script>
import CardFlip from "./CardCom.vue";
export default {
  components: {
    CardFlip,
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    onBackToMainScreen() {
      this.$emit("onBackToMainScreen");
    },
    async checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onAddClassDisables();
        this.$refs[`card-${this.rules[1].index}`][0].onAddClassDisables();
        this.rules = [];
        const completedList = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (
          completedList &&
          completedList.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("Wrong");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBack();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBack();
          this.rules = [];
        }, 500);
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}
.screen__inner {
  margin: 32px auto;
  width: 424px;
  display: flex;
  flex-wrap: wrap;
}
.card {
  flex-direction: row;
}
.btn__back {
  display: inline-block;
  margin: 24px;
  cursor: pointer;
  color: rgb(255, 196, 0);
}
.btn__back:hover {
  text-decoration: underline;
}
</style>
