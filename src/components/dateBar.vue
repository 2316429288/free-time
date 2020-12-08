<template>
  <nav style="padding: 1em 0">
    <span class="font-weight-bold pl-3" style="font-size: 25px">Today</span>
    <span class="text-secondary text-left p-1">{{ dayOfweeks }}</span>
    <span class="text-secondary text-left">{{ dayOfMonths }}</span>
    <span class="text-secondary text-left p-1">{{ dayOfDays }}</span>
    <todo-modal></todo-modal>
  </nav>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import todoModal from "./todoModal.vue";

export default defineComponent({
  name: "dateBar",
  setup() {
    const date = new Date();
    const months = [
      "Jan",
      "Feb",
      "Mar",
      "Apr",
      "May",
      "Jun",
      "Jul",
      "Aug",
      "Sept",
      "Oct",
      "Nov",
      "Dec",
    ];
    const week = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];
    const dayOfweeks = week[date.getDay()];
    const dayOfMonths = months[date.getMonth()];
    const dayOfDays = date.getDate();
    return { dayOfweeks, dayOfMonths, dayOfDays };
  },
  components: {
    todoModal
  }
});
</script>