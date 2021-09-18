<template>
  <div class="row">
    <div class="col">
      <h3>Draggable 1</h3>
      <draggable
        @change="log"
        :sort=false
        :list="list1"
        v-bind="dragOptions"
        :group="{name: 'draggableGroup', pull: 'clone', put: false}"
      >
        <div
          :key="element.name"
          v-for="element in list1"
          class="list-group-item"
        >
          <FormItem :name="element.name"/>
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
          :key="element.name + index"
        >
          <FormItem :name="element.name"/>
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
import FormItem from './FormItem';
import RawDisplayer from './RawDisplayer';

export default {
  name: "HelloWord",
  components: {
    draggable,
    FormItem,
    RawDisplayer
  },
  data() {
    return {
      list1: [
        {name: "text", id: 1},
        {name: "textarea", id: 2},
        {name: "multiSelect", id: 3},
        {name: "select", id: 4},
        {name: "date", id: 5},
        {name: "time", id: 6},
        {name: "dateTime", id: 7},
        {name: "inputNumber", id: 8},
      ],
      list2: [
        {name: "text", id: 11},
        {name: "textarea", id: 22},
        {name: "multiSelect", id: 33},
        {name: "select", id: 44},
        {name: "date", id: 55},
        {name: "time", id: 66},
        {name: "dateTime", id: 77},
        {name: "inputNumber", id: 88},
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

.list-group-item {
  width: 300px;
  padding: 5px;
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
