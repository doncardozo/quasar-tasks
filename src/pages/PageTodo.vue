<template>
  <q-page class="q-pa-md">
    <q-list
      separator
      borderer>
      <Tasks 
        v-for="(task, key) in tasks"
        :key="key"
        :task="task"
        :id="key"
      />
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
import AddTask from 'components/Tasks/Modals/AddTask'

export default {
  name: 'PageTodo',
  components: {
    Tasks,
    AddTask
  },
  data(){
    return {
      showAddTask: false
    }
  },
  computed: {
    ...mapGetters('tasks', ['tasks'])
  }
}
</script>
