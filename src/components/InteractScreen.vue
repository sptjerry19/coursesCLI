<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardContext.length) - 16) * 3) / 4) *
            Math.sqrt(cardContext.length) +
          16 * Math.sqrt(cardContext.length)
        }px`,
      }"
    >
      <!-- <h2>interact open</h2> -->
      <CardFlip
        v-for="(card, index) in cardContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardContext="cardContext"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>

<script>
import CardFlip from "./CardGame.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
      countEnable: 0,
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) {
        return false;
      }
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("right");
        // count right++
        this.countEnable++;
        if (this.countEnable === this.cardContext.length / 2) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 800);
        }
        // disabled event click
        this.$refs[`card-${this.rules[0].index}`][0].onEnableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableMode();
        //reset rules -> []
        this.rules = [];
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          console.log("wrong");
          // close two card
          this.$refs[`card-${this.rules[0].index}`][0].onCloseCard();
          this.$refs[`card-${this.rules[1].index}`][0].onCloseCard();
          // reset array rules -> []
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
}

.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
