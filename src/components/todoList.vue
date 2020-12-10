<template>
  <ul class="list-group" v-if="todoList.length">
    <li
      class="list-group-item w-75 ml-3"
      v-for="item in todoList"
      :key="item"
      @click="wellDown"
    >
      <button
        type="button"
        id="addStrikeBtn"
        class="lit-btn-transition-scale"
        :class="downBtn"
      ></button>
      <span :class="isDown">{{ item }}</span>
      <button type="button" id="deleteBtn" class="deleteBtn"></button>
    </li>
  </ul>
  <div class="pt-5 mt-5" v-else>
    <h3 class="text-center" style="color: #db7093">从心力交瘁到掌控一切</h3>
    <h3 class="text-center" style="color: #db7093">现在开始你的第一条便签</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import mitt from "mitt";
import "../css/lit-animation.css";

// 创建mitt实例
export const emitter = mitt();
// 定义数据类型
type validateItem = string;
type validateList = validateItem[];

export default defineComponent({
  name: "todoList",
  setup() {
    // 控制样式
    const isDown = {
      down: false
    };
    const downBtn = ref({
      hasNike: false,
      noNike: true
    });
    // 生成todoList
    const todoList = ref<validateList>([]);
    const callback = (task?: validateItem) => {
      if (task) {
        todoList.value.push(task);
      }
    };
    // mitt传值
    emitter.on("list-created", callback);
    // onUnmounted(() => {
    //   emitter.off("list-created", callback);
    // });
    // Li按钮单击事件
    const wellDown = (e: MouseEvent) => {
      if (e.target) {
        const targetEle = e.target as HTMLElement;
        const liItem = targetEle.parentNode;
        if (targetEle.id === "deleteBtn") {
          liItem?.parentNode?.removeChild(liItem);
        } else if (targetEle.id === "addStrikeBtn") {
          // 添加下划线(未完成)
          downBtn.value.hasNike = !downBtn.value.hasNike;
          downBtn.value.noNike = !downBtn.value.noNike;
        } else {
          return;
        }
      }
      // todoList.value.splice();
    };
    return {
      todoList,
      wellDown,
      isDown,
      downBtn
    };
  }
});
</script>
<style>
.list-group-item {
  padding: 1em 1em 0.5em;
  border-top: 0;
  border-left: 0;
  border-right: 0;
}
.list-group-item:last-child {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}
.hasNike {
  background-image: url("~@/assets/Success.png");
}
.noNike {
  background-image: url("~@/assets/Add.svg");
}
.deleteBtn {
  background-image: url(~@/assets/Delete.svg);
  height: 1.3em;
  width: 1.3em;
  top: 0.5em;
  float: right;
}
.noNike,
.hasNike {
  height: 1.5em;
  width: 1.5em;
  top: 0.3em;
  margin-right: 0.4em;
}
.noNike,
.hasNike,
.deleteBtn {
  background-color: transparent;
  border: none;
  border-radius: 50%;
  background-size: cover;
  position: relative;
}
.list-button:focus {
  outline: none;
}
.list-button:hover {
  cursor: auto;
}
[type="button"]:not(:disabled),
[type="reset"]:not(:disabled),
[type="submit"]:not(:disabled),
button:not(:disabled) {
  cursor: auto;
}
.down {
  text-decoration: line-through;
}
</style>
