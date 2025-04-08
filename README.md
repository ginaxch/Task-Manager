### Vue Task Manager

This Vue.js project implements a task management system using Vuetify. It features functionalities to add, update, delete, and mark tasks as complete. The application ensures that tasks marked as complete cannot be updated, and any modifications can be discarded by using a cancel button in the task dialog.
Features

- Add Tasks: Users can add new tasks with details such as title, description, deadline, and priority.
- Update Tasks: Tasks that are not marked as complete can be updated.
- Delete Tasks: Any task can be deleted.
- Mark as Complete: Tasks can be marked as complete.
- Dynamic UI Updates: The update button is hidden for tasks that are marked as complete.
- Cancel Modifications: Any changes made in the update dialog can be canceled without affecting the original data.

## Prerequisites
Node.js (LTS version)
Vue CLI installed globally (npm install -g @vue/cli)
