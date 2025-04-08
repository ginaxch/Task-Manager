<template>
<v-data-table :headers="headers" :items="tasks" class="elevation-1">
  <template v-slot:item.action="{ item }">
    <!-- Only show the update button if the task is not complete -->
    <v-btn icon v-if="!item.isComplete" @click="editTask(item)">
      <v-icon>mdi-pencil</v-icon>
    </v-btn>
    <v-btn icon @click="deleteTask(item)">
      <v-icon>mdi-delete</v-icon>
    </v-btn>
  </template>
  <template v-slot:item.isComplete="{ item }">
    <v-checkbox v-model="item.isComplete" @change="completeTask(item)"></v-checkbox>
  </template>
</v-data-table>
</template>

<script>
export default {
data() {
  return {
    tasks: [],
    headers: [
      { text: 'Title', value: 'title' },
      { text: 'Description', value: 'description' },
      { text: 'Deadline', value: 'deadline' },
      { text: 'Priority', value: 'priority' },
      { text: 'Complete?', value: 'isComplete' },
      { text: 'Actions', value: 'action', sortable: false }
    ]
  };
},
methods: {
  addTask(task) {
    this.tasks.push(task);
  },
  editTask(task) {
    this.$emit('edit', task);
  },
  deleteTask(task) {
    const index = this.tasks.indexOf(task);
    if (index > -1) {
      this.tasks.splice(index, 1);
    }
  },
  completeTask(task) {
    task.isComplete = !task.isComplete; // Toggle complete state
    // If a task is marked complete, remove the ability to edit it
    if (task.isComplete) {
      this.$emit('update');
    }
  }
}
}
</script>
