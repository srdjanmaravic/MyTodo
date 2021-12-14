<template>
  <div class="home">
    <field-add-tasks />
    <list-tasks v-if="$store.state.tasks.length" />
    <no-task v-else />
    <done-sorting v-if="$store.state.sorting"></done-sorting>
  </div>
</template>

<script>
import FieldAddTask from "@/components/Todo/FieldAddTask.vue";
import ListTasks from "@/components/Todo/ListTasks.vue";
import NoTask from "@/components/Todo/NoTask.vue";
import ButtonDoneSorting from "@/components/Todo/Dialogs/ButtonDoneSorting.vue";
export default {
  name: "Todo",

  components: {
    "field-add-tasks": FieldAddTask,
    "list-tasks": ListTasks,
    "no-task": NoTask,
    "done-sorting": ButtonDoneSorting,
  },
};
</script>
