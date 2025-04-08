<template>
<v-app>
  <v-app-bar app dense>
    <v-toolbar-title>FRAMEWORKS</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn icon @click="showAddDialog">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
  </v-app-bar>

  <v-main>
    <task-table ref="taskTable"></task-table>
  </v-main>

  <task-dialog ref="taskDialog" @save="handleSave" @update="handleUpdate"/>
</v-app>
</template>

<script>
import TaskTable from './TaskTable.vue';
import TaskDialog from './TaskDialog.vue';

export default {
components: {
  TaskTable,
  TaskDialog
},
methods: {
  showAddDialog() {
    this.$refs.taskDialog.open();
  },
  handleSave(task) {
    this.$refs.taskTable.addTask(task);
  },
  handleUpdate(task) {
    this.$refs.taskTable.updateTask(task);
  }
}
}
</script>
