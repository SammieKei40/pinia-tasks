<template>
  <main>
    <header>
      <img src="./assets/logo.svg" alt="">
      <h1>{{ taskStore.name }}</h1>
    </header>

    <div class="new-task-form">
      <taskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Favs tasks</button>
    </nav>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks left to do</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} tasks left to do</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task"/>
      </div>
    </div>
  </main>
</template>

<script>
import TaskForm from './components/TaskForm.vue'
import TaskDetails from "./components/TaskDetails.vue"
import { useTaskStore } from './stores/TaskStore';
import { ref } from "vue";

  export default {
    components: {TaskDetails, TaskForm},
    setup(){
      const taskStore = useTaskStore()
      const filter = ref('all')


      return {taskStore, filter}
    }
  }
</script>
