<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardContext.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) / 4
      }px`,
    }"
  >
    <div
      class="card__inner"
      @click="onToggleFlip"
      :class="{ 'is-flipped': isFlipped }"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
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
      type: [String, Number, Object, Array],
      required: true,
    },
    cardContext: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisabled: false,
    };
  },
  methods: {
    onToggleFlip() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onCloseCard: function () {
      this.isFlipped = false;
    },
    onEnableMode() {
      this.isDisabled = true;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}

.card.disabled .card__inner {
  cursor: default;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  box-shadow: -3px 1px 20px 3px rgb(54 5 249 / 20%);
}

.card__face--front .card__content {
  background: url("../assets/logo.png") no-repeat center center;
  background-size: 30px 30px;
  height: 100%;
  width: 100%;
  background-color: #95bbdd;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--back .card__content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
  background-color: #dff0ff;
}
</style>
