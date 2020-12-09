<template>
  <ul class="list-group" v-if="todoList.length" @click="wellDown">
    <li
      class="list-group-item w-75 ml-3"
      v-for="(item, index) in todoList"
      :key="index"
      ref="listRef"
    >
      <button
        type="button"
        class="list-button lit-btn-transition-scale"
      ></button>
      {{ item }}
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
    const listRef = ref(null);
    const todoList = ref<validateList>([]);
    const callback = (task?: validateItem) => {
      if (task) {
        todoList.value.push(task);
        console.log(listRef)
      }
    };
    emitter.on("list-created", callback);
    // onUnmounted(() => {
    //   emitter.off("list-created", callback);
    // });
    const wellDown = (index: number) => {
      console.log(index);
      todoList.value.splice(index, 1);
    };
    return {
      todoList,
      wellDown,
      listRef
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
.list-button {
  background-image: url("~@/assets/Success.svg");
  background-color: transparent;
  border: none;
  border-radius: 50%;
  background-size: cover;
  height: 2em;
  width: 2em;
  position: relative;
  top: 0.5em;
  margin-right: 0.4em;
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
</style>
