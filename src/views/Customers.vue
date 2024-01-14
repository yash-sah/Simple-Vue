<template>
    <div>
      <h2>Task List</h2>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <input type="checkbox" v-model="task.completed" />
          {{ task.description }}
        </li>
      </ul>
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tasks: [],
        newTask: '',
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({ description: this.newTask, completed: false });
          this.newTask = '';
        }
      },
    },
  };
  </script>
  