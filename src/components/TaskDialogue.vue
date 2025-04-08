<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <v-card>
      <v-card-title>
        <span class="headline">{{ formTitle }}</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field v-model="task.title" label="Title" :rules="[rules.required, rules.unique]" required></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field v-model="task.description" label="Description" :rules="[rules.required]" required></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-menu ref="menu" v-model="menu" :close-on-content-click="false" :nudge-right="40" transition="scale-transition" offset-y min-width="auto">
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field v-model="task.deadline" label="Pick a date" prepend-icon="mdi-calendar" readonly v-bind="attrs" v-on="on"></v-text-field>
                </template>
                <v-date-picker v-model="task.deadline" no-title @input="menu = false"></v-date-picker>
              </v-menu>
            </v-col>
            <v-col cols="12">
              <v-radio-group v-model="task.priority" label="Priority">
                <v-radio label="Low" value="low"></v-radio>
                <v-radio label="Medium" value="medium"></v-radio>
                <v-radio label="High" value="high"></v-radio>
              </v-radio-group>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
        <v-btn color="blue darken-1" text @click="save">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      dialog: false,
      formTitle: 'Add Task',
      rules: {
        required: value => !!value || 'Required.',
        unique: value => {
          const exists = this.tasks.some(t => t.title === value);
          return !exists || 'Title must be unique.';
        }
      }
    };
  },
  methods: {
    open() {
      this.dialog = true;
    },
    close() {
      this.dialog = false;
    },
    save() {
      if (this.validate()) {
        this.dialog = false;
        this.$emit('save', this.task);
      }
    },
    validate() {
      return this.task.title && this.task.description && this.task.deadline && this.task.priority;
    }
  }
}
</script>
