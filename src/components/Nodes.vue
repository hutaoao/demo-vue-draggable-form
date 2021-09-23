<template>
  <div class="nodeBox">
    <img class="icon" :src="require(`../assets/icon/${this.type}.png`)" alt="icon">
    <span class="node">{{title}}</span>
  </div>
</template>

<script>
export default {
  name: "Nodes",
  props: {
    title: {
      type: String
    },
    type: {
      type: String
    }
  },
}
</script>

<style scoped>
.nodeBox {
  cursor: move;
  width: 80px;
  height: 80px;
  display: flex;
  font-size: 12px;
  flex-flow: column;
  align-items: center;
  justify-content: center;
  border: 1px solid #eef2f8;
}

.nodeBox:hover {
  background: #e1f4ff;
}

.icon {
  width: 20px;
  margin-bottom: 5px;
}
</style>
