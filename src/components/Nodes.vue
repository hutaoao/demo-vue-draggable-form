<template>
  <el-tag class="tag">{{type}}</el-tag>
</template>

<script>
export default {
  name: "Nodes",
  props: {
    type: {
      type: String
    }
  },
}
</script>

<style scoped>
.tag {
  margin: 8px;
}
</style>
