<template>
  <div class="row">
    <div class="col">
      <h3>Draggable 1</h3>
      <draggable
        @change="log"
        :sort=false
        :list="list1"
        class="draggableBox"
        v-bind="dragOptions"
        :group="{name: 'draggableGroup', pull: 'clone', put: false}"
      >
        <div
          :key="element.type"
          v-for="element in list1"
          class="list-group-item2"
        >
          <Nodes :type="element.name"/>
        </div>
      </draggable>
    </div>

    <div class="col" style="margin-right: 80px">
      <h3>Draggable 2</h3>
      <draggable
        @change="log"
        :list="list2"
        v-bind="dragOptions"
        group="draggableGroup"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list2"
          :key="element.type + index"
        >
          <FormItem :type="element.type"/>
          <i class="el-icon-delete" @click="delItem(index)"/>
        </div>
      </draggable>
    </div>
    <raw-displayer class="col" :value="list1" title="List1 Data"/>
    <raw-displayer class="col" :value="list2" title="List2 Data"/>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import Nodes from "./Nodes";
import FormItem from './FormItem';
import RawDisplayer from './RawDisplayer';

export default {
  type: "HelloWord",
  components: {
    Nodes,
    draggable,
    FormItem,
    RawDisplayer
  },
  data() {
    return {
      list1: [
        {type: "text", name: '单行文本', id: 1},
        {type: "textarea", name: '多行文本', id: 2},
        {type: "multiSelect", name: '多选下拉', id: 3},
        {type: "select", name: '单选下拉', id: 4},
        {type: "date", name: '日期组件', id: 5},
        {type: "time", name: '时间组件', id: 6},
        {type: "dateTime", name: '日期时间', id: 7},
        {type: "inputNumber", name: '数字组件', id: 8},
      ],
      list2: [
        {type: "text", id: 11},
        {type: "textarea", id: 22},
        {type: "multiSelect", id: 33},
        {type: "select", id: 44},
        {type: "date", id: 55},
        {type: "time", id: 66},
        {type: "dateTime", id: 77},
        {type: "inputNumber", id: 88},
      ]
    };
  },
  computed: {
    dragOptions() {
      return {
        animation: 500,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  },
  methods: {
    log: function (evt) {
      window.console.log(evt);
    },
    delItem(index) {
      let newList = this.list2;
      newList.splice(index, 1);
      this.list2 = newList;
    }
  }
};
</script>
<style scoped>
.row {
  display: flex;
  flex-flow: row;
}

.col {
  margin: 15px;
}

.draggableBox {
  display: flex;
  flex-wrap: wrap;
  width: 180px;
  padding: 20px;
  border: 1px solid #eee;
}

.list-group-item {
  width: 300px;
  padding: 6px;
  border: 1px solid #eee;
  position: relative;
}

.el-icon-delete {
  position: absolute;
  top: 20px;
  right: -30px;
  cursor: pointer;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
</style>
