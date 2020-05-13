<template>
  <q-page class="q-pa-md">
    <q-list
      separator
      borderer>

      <div v-if="Object.keys(tasksTodo).length">
        <q-banner dense class="bg-orange text-white text-center">
          Todo tasks
        </q-banner>      
        <Tasks 
          v-for="(task, key) in tasksTodo"
          :key="key"
          :task="task"
          :id="key"
        />
      </div>

      <div :class="Object.keys(tasksTodo).length ? 'q-mt-lg' : ''" v-if="Object.keys(tasksCompleted).length">
        <q-banner dense class="bg-green text-white text-center">
          Completed tasks
        </q-banner>
        <TasksCompleted
          v-for="(task, key) in tasksCompleted"        
          :key="key"
          :task="task"
          :id="key"
        />      
      </div>
      <div class="absolute-bottom text-center q-mb-lg">
        <q-btn 
          @click="showAddTask = true"
          round
          color="primary"
          size="24px"
          icon="add"
          />
      </div>
      <q-dialog v-model="showAddTask">
        <AddTask @close="showAddTask = false" />
      </q-dialog>
    </q-list>
  </q-page>
</template>

<script>
import { mapGetters } from 'vuex'
import Tasks from 'components/Tasks/Tasks'
import TasksCompleted from 'components/Tasks/TasksCompleted'
import AddTask from 'components/Tasks/Modals/AddTask'

export default {
  name: 'PageTodo',
  components: {
    Tasks,
    TasksCompleted,
    AddTask
  },
  data(){
    return {
      showAddTask: false
    }
  },
  computed: {
    ...mapGetters('tasks', ['tasksTodo','tasksCompleted'])
  }
}
</script>
