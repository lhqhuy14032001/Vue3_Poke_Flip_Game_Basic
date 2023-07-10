<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardContext.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        ((((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) / 4) * 2
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ is__flipped: isFlipped }"
      @click="onToggleCard"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) /
              4 /
              3
            }px
            ${
              (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) /
              4 /
              3
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isDisabled: false,
      isFlipped: false,
    };
  },
  methods: {
    onToggleCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFlipBack() {
      return (this.isFlipped = false);
    },
    onAddClassDisables() {
      return (this.isDisabled = true);
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 16px;
  margin-bottom: 16px;
  width: 90px;
  height: 120px;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is__flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 16px;
  padding: 16px;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
  color: #ffff;
}
.card__face--front .card__content {
  background: url(../assets//images/icon_back.png) no-repeat center center;
  width: 100%;
  height: 100%;
}
.card__face--back .card__content {
  width: 100%;
  height: 100%;
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
}
.card__face--back {
  background-color: #212121;
  transform: rotateY(-180deg);
}
.card.disabled .card__inner {
  cursor: default;
}
</style>
