<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <p>Select mode to start game</p>
    <div class="actions">
      <button @click="onStartGame(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStartGame(36)">
        <span>6x6</span>
        <span>Medium</span>
      </button>
      <button @click="onStartGame(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStartGame(100)">
        <span>10x10</span>
        <span>Supper Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStartGame(totalOfBlock) {
      this.$emit("onStartGame", { totalOfBlock });
    },
  },
};
</script>

<style scoped>
button {
  width: 100px;
  height: 60px;
  margin: 10px 20px;
  box-shadow: 5px 6px 14px 2px rgba(32, 54, 248, 0.6);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: aliceblue;
  border-radius: 20px;
  border: none;
  padding: 20px 0;
}
button:hover {
  background-color: rgb(100, 179, 248);
  cursor: pointer;
}
.actions {
  display: flex;
  align-items: center;
  justify-content: center;
}
h1 {
  color: aliceblue;
  padding: 20px 0;
}
p {
  color: aliceblue;
  padding: 20px 0;
}
</style>
