<template>
  <div class="main-screen">
    <section class="header">
      <h1>POKE MEMORIES</h1>
      <h3>Select mode to start game</h3>
    </section>
    <section class="body">
      <div class="mode-list">
        <div class="mode-item" @click="onStart(16)">
          4x4<br />
          Easy
        </div>
        <div class="mode-item" @click="onStart(36)">
          6x6<br />
          Normal
        </div>
        <div class="mode-item" @click="onStart(64)">
          8x8<br />
          Hard
        </div>
        <div class="mode-item" @click="onStart(100)">
          10x10<br />
          Super Hard
        </div>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style scoped lang="css">
.header {
  margin: 50px 0;
}
.header h1,
.header h3 {
  color: #fff;
  text-align: center;
}
.header h1 {
  font-size: 72px;
}
.header h3 {
  font-size: 32px;
}
.body .mode-list {
  display: flex;
  justify-content: center;
}
.mode-item {
  display: flex;
  margin: 0 12px;
  padding: 8px 16px;
  height: 150px;
  width: 150px;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: transparent;
  color: #fff;
  border-radius: 8px;
  border: solid 1px #fff;
  font-size: 24px;
  cursor: pointer;
}
.mode-item:hover {
  background-color: #f3f3f3;
  color: #212121;
}
</style>
