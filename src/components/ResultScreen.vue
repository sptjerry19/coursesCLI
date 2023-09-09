<template>
  <div class="resultGame">
    <h2>complete</h2>
    <p>Time: {{ Math.floor(timer / 1000) }} seconds</p>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style scoped>
.resultGame {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  position: absolute;
  height: 400px;
  width: 400px;
  background-color: #c9c9c9;
  box-shadow: 20px 20px 20px 1px #9b9b9b;
  border-radius: 20px;
}
button {
  width: 200px;
  height: 100px;
  font-size: 30px;
  font-family: cursive;
}
h2 {
  font-family: cursive;
  font-size: 50px;
}
</style>
