<template>
  <div>
    <el-form ref="form" :model="form" label-width="80px">
      <el-form-item label="单行文本" v-if="type === 'text'">
        <el-input
          class="el"
          placeholder="请输入内容"
          v-model="form.textValue"
        ></el-input>
      </el-form-item>
      <el-form-item label="多行文本" v-if="type === 'textarea'">
        <el-input
          class="el"
          type="textarea"
          placeholder="请输入内容"
          v-model="form.textareaValue"
        ></el-input>
      </el-form-item>
      <el-form-item label="多选" v-if="type === 'multiSelect'">
        <el-select
          multiple
          collapse-tags
          class="el"
          placeholder="请选择"
          v-model="form.multiValue"
        >
          <el-option label="选项1" value="1"></el-option>
          <el-option label="选项2" value="2"></el-option>
          <el-option label="选项3" value="3"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="下拉列表" v-if="type === 'select'">
        <el-select
          class="el"
          placeholder="请选择"
          v-model="form.selectValue"
        >
          <el-option label="选项1" value="1"></el-option>
          <el-option label="选项2" value="2"></el-option>
          <el-option label="选项3" value="3"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="日期" v-if="type === 'date'">
        <el-date-picker
          type="date"
          placeholder="选择日期"
          v-model="form.dateValue"
        ></el-date-picker>
      </el-form-item>
      <el-form-item label="时间" v-if="type === 'time'">
        <el-time-select
          :picker-options="{
            start: '08:30',
            step: '00:15',
            end: '18:30'
          }"
          placeholder="选择时间"
          v-model="form.timeValue"
        ></el-time-select>
      </el-form-item>
      <el-form-item label="日期时间" v-if="type === 'dateTime'">
        <el-date-picker
          v-model="form.datetimeValue"
          type="datetime"
          placeholder="选择日期时间"
        ></el-date-picker>
      </el-form-item>
      <el-form-item label="数值" v-if="type === 'inputNumber'">
        <el-input-number
          class="el"
          v-model="form.inputNumValue"
        ></el-input-number>
      </el-form-item>
      <el-form-item label="图片附件" v-if="type === 'img'">

      </el-form-item>
      <el-form-item label="文档附件" v-if="type === 'file'">

      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  type: "FormItem",
  props: {
    type: {
      type: String
    }
  },
  data() {
    return {
      form: {
        textValue: '',
        textareaValue: '',
        multiValue: '',
        inputNumValue: '',
        selectValue: '',
        radioValue: '',
        checkValue: '',
        dateValue: '',
        timeValue: '',
        datetimeValue: ''
      }
    }
  }
}
</script>

<style scoped>
.el {
  width: 100%;
}
</style>
