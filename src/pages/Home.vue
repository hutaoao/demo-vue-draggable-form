<template>
  <div class="box">
    <div class="header">
      <h4 class="header_title">自定义表单</h4>
      <div>
        <el-button size="small" type="primary">保存</el-button>
        <el-button size="small" type="success">预览</el-button>
      </div>
    </div>
    <div class="content">
      <div class="component_box">
        <h5 class="component_sub_title">常用组件</h5>
        <draggable
          @change="log"
          :sort=false
          class="draggableBox"
          v-bind="dragOptions"
          :list="this.componentList"
          :group="{name: 'draggableGroup', pull: 'clone', put: false}"
        >
          <div
            :key="element.type"
            class="list-group-item2"
            v-for="element in this.componentList"
          >
            <Nodes :title="element.title" :type="element.type"/>
          </div>
        </draggable>
      </div>

      <div class="canvas_box" @click="resetActive">
        <div class="canvas">
          <draggable
            @change="log"
            v-bind="dragOptions"
            :list="this.canvasList"
            group="draggableGroup"
          >
            <div
              class="canvas_item"
              v-for="(element, index) in this.canvasList"
              :key="element.type + index"
              :class="activeIndex === index && 'active'"
              @click.stop="handleGroupItem(index, element)"
            >
              <FormItem :element="element"/>
              <!--<i class="el-icon-delete" @click="delItem(index)"/>-->
            </div>
          </draggable>
        </div>
      </div>
      <div class="configuration_box">
        <div class="edit" v-if="activeIndex > -1">
          <Editor :editElement="editElement"/>
        </div>
      </div>
      <!--<raw-displayer class="col" :value="this.componentList" title="List1 Data"/>
            <raw-displayer class="col" :value="this.canvasList" title="List2 Data"/>-->
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import {mapActions, mapState} from 'vuex';
import Nodes from "../components/Nodes";
import Editor from "../components/Editor";
import FormItem from '../components/FormItem';
// import RawDisplayer from '../components/RawDisplayer';

export default {
  type: "HelloWord",
  components: {
    Nodes,
    Editor,
    FormItem,
    draggable,
    // RawDisplayer
  },
  data() {
    return {
      editElement: {},
      activeIndex: -1,
    };
  },
  computed: {
    ...mapState(['componentList', 'canvasList']),
    dragOptions() {
      return {
        animation: 500,
        group: "description",
        disabled: false,
        dragClass: "dragItem",
        ghostClass: "ghostItem",
        chosenClass: "chosenItem",
      };
    }
  },
  methods: {
    ...mapActions(['handleCanvas']),
    log: function (evt) {
      window.console.log(evt);
    },
    delItem(index) {
      let newList = this.canvasList;
      newList.splice(index, 1);
      this.handleCanvas(newList);
    },
    handleGroupItem(index, element) {
      this.activeIndex = index;
      this.editElement = element;
    },
    resetActive() {
      this.activeIndex = -1;
    }
  }
};
</script>
<style scoped>
.box {
  display: flex;
  flex-flow: column;
}

.header {
  height: 60px;
  line-height: 60px;
  padding: 0 20px;
  z-index: 99;
  display: flex;
  justify-content: space-between;
  box-shadow: 0 0 4px 0 rgb(0 0 0 / 16%);
}

.header_title {

}

.content {
  flex: 1;
  display: flex;
  flex-flow: row;
  justify-content: space-between;
}

.component_box {
  width: 300px;
  overflow-y: scroll;
  height: calc(100vh - 60px);
}

.component_sub_title {
  padding: 20px 0 0 20px;
}

.canvas_box {
  flex: 1;
  display: flex;
  justify-content: center;
  background-color: #eef2f8;
  height: calc(100vh - 60px);
  overflow-y: scroll;
  position: relative;
}

.canvas_box .canvas {
  width: 360px;
  position: absolute;
  background-color: #ffffff;
}

.configuration_box {
  width: 340px;
  overflow-y: scroll;
  height: calc(100vh - 60px);
}

.edit {
  padding: 10px;
  min-height: 500px;
  border: 1px solid #eeeeee;
}

.draggableBox {
  display: flex;
  flex-wrap: wrap;
  padding: 20px;
}

.canvas_item {
  padding: 6px;
  position: relative;
  cursor: move;
  border: 1px solid #ffffff;
}

.canvas_item:hover {
  border-color: #89d6ff;
}

.canvas_item.active {
  border-color: #0fb4ff;
}

.el-icon-delete {
  position: absolute;
  top: 20px;
  right: -30px;
  cursor: pointer;
}

.ghostItem {
  opacity: 0.5;
  background: #c8ebfb;
}

.chosenItem {
  box-shadow: 0 0 15px #999999;
}
</style>
