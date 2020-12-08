<template>
  <ul class="list-group">
    <!-- <li class="list-group-item w-75 ml-3" v-for="task in dateArr" :key="task">
      <img class="list-item-img" src="../assets/Success.svg" />{{ task }}
    </li> -->
  </ul>
  <ul class="list-group">
    <li class="list-group-item w-75 ml-3">
      <img class="list-item-img" src="../assets/Success.svg" />{{ todo }}
    </li>
    <li class="list-group-item w-75 ml-3">
      <img class="list-item-img" src="../assets/Success.svg" />{{ todo }}
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, onUnmounted, ref} from "vue";
import mitt from "mitt";

// 创建mitt实例
export const emitter = mitt();
type validateStr = string;
export default defineComponent({
  name: "todoList",
  setup() {
    const dateArr = ref(['帅气', '就是帅气','无比帅气'])
    const todo = "今天剪头发";
    const validateArr = ref([])
    const callback = () => {
      // if () {
      //   console.log(validateArr)
      // }
    };
    emitter.on("list-created", callback);
    // onUnmounted(() => {
    //   emitter.off("list-created", callback);
    // });
    return {
      todo,
      validateArr,
      dateArr
    };
  },
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
.list-item-img {
  width: 1.5em;
  padding-bottom: 0.175em;
  margin-right: 0.5em;
}
</style>
