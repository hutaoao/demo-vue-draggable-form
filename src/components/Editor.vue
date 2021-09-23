<template>
  <div>
    <el-form ref="form" :model="form" size="mini" label-width="80px">
      <el-form-item label="标题">
        <el-input
          class="el"
          v-model="editElement.title"
        ></el-input>
      </el-form-item>
      <el-form-item label="占位符">
        <el-input
          class="el"
          v-model="editElement.placeholder"
        ></el-input>
      </el-form-item>
      <el-form-item label="默认文本">
        <el-input
          class="el"
          v-model="editElement.defaultValue"
        ></el-input>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import {mapState, mapActions} from "vuex";

export default {
  name: "Editor",
  props: {
    editElement: {
      type: Object,
    }
  },
  computed: {
    ...mapState(['canvasList']),
  },
  data() {
    return{
      form: {
        title: '',
      }
    }
  },
  methods: {
    ...mapActions(['handleCanvas']),
    handleText(e) {
      console.log(e);
    }
  },
}
</script>

<style scoped>

</style>
