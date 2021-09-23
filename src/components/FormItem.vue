<template>
  <div class="form_box">
    <el-form ref="form" :model="form" label-width="80px">
      <el-form-item :label="element.title" v-if="element.type === 'text'">
        <el-input
          readonly
          class="el"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        ></el-input>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'textarea'">
        <el-input
          readonly
          class="el"
          element.type="textarea"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        ></el-input>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'multiSelect'">
        <el-select
          readonly
          multiple
          collapse-tags
          class="el"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        >
          <el-option label="选项1" value="1"></el-option>
          <el-option label="选项2" value="2"></el-option>
          <el-option label="选项3" value="3"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'select'">
        <el-select
          class="el"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        >
          <el-option label="选项1" value="1"></el-option>
          <el-option label="选项2" value="2"></el-option>
          <el-option label="选项3" value="3"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'cascader'">
        <el-cascader
          style="width: 100%;"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
          :options="options"
        ></el-cascader>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'date'">
        <el-date-picker
          style="width: 100%;"
          element.type="date"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        ></el-date-picker>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'time'">
        <el-time-select
          style="width: 100%;"
          :picker-options="{
            start: '08:30',
            step: '00:15',
            end: '18:30'
          }"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        ></el-time-select>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'dateTime'">
        <el-date-picker
          style="width: 100%;"
          :placeholder="element.placeholder"
          v-model="element.defaultValue"
        ></el-date-picker>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'number'">
        <el-input-number
          class="el"
          v-model="form.defaultValue"
        ></el-input-number>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'integer'">
        <el-input-number
          class="el"
          :step="0.01"
          v-model="form.defaultValue"
        ></el-input-number>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'img'">
        <el-upload
          class="upload-demo"
          action="https://jsonplaceholder.typicode.com/posts/"
          :on-preview="handlePreview"
          :on-remove="handleRemove"
          :file-list="fileList"
          list-type="picture">
          <el-button size="small" type="primary">点击上传</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>
      <el-form-item :label="element.title" v-if="element.type === 'file'">
        <el-upload
          class="upload-demo"
          action="https://jsonplaceholder.typicode.com/posts/"
          :on-preview="handlePreview"
          :on-remove="handleRemove"
          :before-remove="beforeRemove"
          multiple
          :limit="3"
          :on-exceed="handleExceed"
          :file-list="fileList">
          <el-button size="small" type="primary">点击上传</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "FormItem",
  props: {
    element: {
      type: Object
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
      },
      options: [{
        value: 'zhinan',
        label: '指南',
        children: [{
          value: 'shejiyuanze',
          label: '设计原则',
          children: [{
            value: 'yizhi',
            label: '一致'
          }, {
            value: 'fankui',
            label: '反馈'
          }, {
            value: 'xiaolv',
            label: '效率'
          }, {
            value: 'kekong',
            label: '可控'
          }]
        }]
      }],
      fileList: [{
        name: 'food.jpeg',
        url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'
      }, {
        name: 'food2.jpeg',
        url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'
      }]
    }
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    handlePreview(file) {
      console.log(file);
    },
    handleExceed(files, fileList) {
      this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
    },
    beforeRemove(file) {
      return this.$confirm(`确定移除 ${file.name}？`);
    },
  }
}
</script>

<style scoped>
.form_box {
  padding: 0 10px;
}

.el {
  width: 100%;
}

/deep/ .el-form-item__label {
  cursor: move;
}

/deep/ .el-form-item {
  margin: 10px 0;
}
</style>
