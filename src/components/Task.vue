<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
        <h2>(Vue JS - Syed)</h2>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" v-model="newTask" @keyup.enter="addTask" />
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <task-item 
          v-bind:task="task" 
          v-for="(task, index) in tasks" 
          :key="task.id"
          @remove="removeTask(index)"
          @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearCompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ inComplete }}</span>
      </div>
      <!-- footer -->
      <div class="footer">
        <p>&copy;</p>
        <p> Developed by Syed Ahmed, 2026. All rights reserved.</p>
      </div>
    </div>
  </div>
</template>

<script>

import TaskItem from "./Task-item.vue";

export default {
  name: "Task",
  props: ["tasks"],
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: ""
    };
  },
  computed: {
    inComplete() {
      return this.tasks.filter(this.inProgress).length;
    },
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          id: this.tasks.length + 1,
          title: this.newTask,
          completed: false,
        });
        this.newTask = "";
      }
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    isCompleted(task) {
      return task.completed;
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    clearAll(){
      this.tasks = [];
    },
    removeTask(index){
      this.tasks.splice(index, 1);
    },
    completeTask(task){
      task.completed = !task.completed;
    }
  }
};
</script>
