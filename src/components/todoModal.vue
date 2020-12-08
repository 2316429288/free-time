<template>
  <!-- Button trigger modal -->
  <div style="float: right; padding: 0.4em 1rem 0 0">
    <img
      class="modal-btn"
      src="../assets/Add.svg"
      data-toggle="modal"
      data-target="#staticBackdrop"
    />
  </div>

  <!-- Modal -->
  <div
    class="modal fade"
    id="staticBackdrop"
    data-backdrop="static"
    data-keyboard="false"
    tabindex="-1"
    role="dialog"
    aria-labelledby="staticBackdropLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered modal-lg">
      <div class="modal-content" style="height: 5em">
        <div class="modal-body" style="height: 5em">
          <form>
            <div class="form-group">
              <input
                class="form-control"
                type="text"
                placeholder="Add a task"
                autocomplete="off"
                onkeydown="if(event.keyCode==13){return false;}"
                v-model="inputRef"
              />
            </div>
          </form>
          <div>
            <button
              type="submit"
              class="btn btn-theme btn-modal"
              data-dismiss="modal"
              @click="newTask"
            >
              添加任务
            </button>
            <button
              type="button"
              class="btn btn-modal"
              data-dismiss="modal"
            >
              取消
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { emitter } from './todoList.vue'

export default defineComponent({
  name: "todoModal",
  props: {
    inputVal: String,
  },
  setup(props, context) {
    const inputRef = ref("");
    const newTask = () => {
      emitter.emit('list-created', inputRef)
      inputRef.value = "";
    };
    return {
      inputRef,
      newTask,
    };
  },
});
</script>

<style>
.modal-btn {
  width: 1.5em;
  border-radius: 50%;
  transition: all 0.5s ease 0s;
}
.modal-btn:hover {
  transition: all 0.5s ease 0s;
  transform: scale(1.2);
}
.btn {
  padding: 0.15em 1em;
  margin: 0em 0.5em;
}
.btn-theme {
  color: #fff;
  background-color: #db7093;
  border-color: #db7093;
}
.btn-theme:hover {
  color: #fff;
  background-color: #c71585;
  border-color: #c71585;
}
.btn-modal {
  font-size: 0.9em;
  float: right;
  padding: 0.25em 1em;
  margin: -0.7em 0.5em;
}
.form-control {
  border: 0;
  margin: -0.5em;
}
.form-control:focus {
  box-shadow: 0 0 0 0;
}
</style>