<template>
    <main>
      <header>
        <h1>Tasks for pinia</h1>

      </header>

      <div class="new-task-form">
        <TaskForm />
      </div>

      <nav class="filter">
        <button @click="filter = 'all'">All tasks</button>
        <button @click="filter = 'favs'">Fav tasks</button>
        <button @click="taskStore.$reset">Reset</button>
      </nav>

      <div class="task-list" v-if="filter === 'all'">
        <p>You have {{ taskStore.totalCount }} tasks left to do</p>
        <div v-for="task in taskStore.tasks">
          <!-- <p>{{ task.title }}</p> -->
          <!-- <p>{{ task.id }}</p> -->
          <TaskDetails :task="task" />
        </div>
      </div>

      <div class="task-list">
        <div v-for="task in taskStore.favs" v-if="filter === 'favs'">
          <p>You have {{ taskStore.favCount }} favs left to do</p>
          <!-- <p>{{ task.title }}</p> -->
          <TaskDetails :task="task" />
        </div>
      </div>
    </main>
    
</template>

<script>

  import { useTaskStore } from './stores/TaskStore';
  import TaskDetails from './components/TaskDetails.vue';
  import TaskForm from './components/TasksForm.vue';
  import { ref } from 'vue';

  export default {

    components: { TaskDetails , TaskForm },

    setup () {
      const taskStore = useTaskStore()

      const filter = ref('all')

      return { taskStore, filter }

    }
  }
</script>